# 合约检查站

## Sway 合约检查点
如果您已正确执行上述步骤，则您的main.sw市场合约应如下所示：

```sway
contract;
 
use std::{
    auth::msg_sender,
    call_frames::msg_asset_id,
    context::{
        msg_amount,
        this_balance,
    },
    asset::transfer,
    hash::Hash,
};
 
struct Item {
    id: u64,
    price: u64,
    owner: Identity,
    metadata: str[20],
    total_bought: u64,
}
 
abi SwayStore {
    // a function to list an item for sale
    // takes the price and metadata as args
    #[storage(read, write)]
    fn list_item(price: u64, metadata: str[20]);
 
    // a function to buy an item
    // takes the item id as the arg
    #[storage(read, write), payable]
    fn buy_item(item_id: u64);
 
    // a function to get a certain item
    #[storage(read)]
    fn get_item(item_id: u64) -> Item;
 
    // a function to set the contract owner
    #[storage(read, write)]
    fn initialize_owner() -> Identity;
 
    // a function to withdraw contract funds
    #[storage(read)]
    fn withdraw_funds();
 
    // return the number of items listed
    #[storage(read)]
    fn get_count() -> u64;
}
 
storage {
    // counter for total items listed
    item_counter: u64 = 0,
 
    // map of item IDs to Items
    item_map: StorageMap<u64, Item> = StorageMap {},
 
    // owner of the contract
    owner: Option<Identity> = Option::None,
}
 
enum InvalidError {
    IncorrectAssetId: AssetId,
    NotEnoughTokens: u64,
    OnlyOwner: Identity,
}
 
impl SwayStore for Contract {
    #[storage(read, write)]
    fn list_item(price: u64, metadata: str[20]) {
        
        // increment the item counter
        storage.item_counter.write(storage.item_counter.try_read().unwrap() + 1);
        
        // get the message sender
        let sender = msg_sender().unwrap();
        
        // configure the item
        let new_item: Item = Item {
            id: storage.item_counter.try_read().unwrap(),
            price: price,
            owner: sender,
            metadata: metadata,
            total_bought: 0,
        };
 
        // save the new item to storage using the counter value
        storage.item_map.insert(storage.item_counter.try_read().unwrap(), new_item);
    }
 
    #[storage(read, write), payable]
    fn buy_item(item_id: u64) {
        // get the asset id for the asset sent
        let asset_id = msg_asset_id();
 
        // require that the correct asset was sent
        require(asset_id == AssetId::base(), InvalidError::IncorrectAssetId(asset_id));
 
        // get the amount of coins sent
        let amount = msg_amount();
 
        // get the item to buy
        let mut item = storage.item_map.get(item_id).try_read().unwrap();
 
        // require that the amount is at least the price of the item
        require(amount >= item.price, InvalidError::NotEnoughTokens(amount));
 
        // update the total amount bought
        item.total_bought += 1;
 
        // update the item in the storage map
        storage.item_map.insert(item_id, item);
 
        // only charge commission if price is more than 0.1 ETH
        if amount > 100_000_000 {
            // keep a 5% commission
            let commission = amount / 20;
            let new_amount = amount - commission;
            // send the payout minus commission to the seller
            transfer(item.owner, asset_id, new_amount);
        } else {
            // send the full payout to the seller
            transfer(item.owner, asset_id, amount);
        }
    }
 
    #[storage(read)]
    fn get_item(item_id: u64) -> Item {
        // returns the item for the given item_id
        return storage.item_map.get(item_id).try_read().unwrap();
    }
 
    #[storage(read, write)]
    fn initialize_owner() -> Identity {
        let owner = storage.owner.try_read().unwrap();
        
        // make sure the owner has NOT already been initialized
        require(owner.is_none(), "owner already initialized");
        
        // get the identity of the sender        
        let sender = msg_sender().unwrap(); 
 
        // set the owner to the sender's identity
        storage.owner.write(Option::Some(sender));
        
        // return the owner
        return sender;
    }
 
    #[storage(read)]
    fn withdraw_funds() {
        let owner = storage.owner.try_read().unwrap();
 
        // make sure the owner has been initialized
        require(owner.is_some(), "owner not initialized");
        
        let sender = msg_sender().unwrap(); 
 
        // require the sender to be the owner
        require(sender == owner.unwrap(), InvalidError::OnlyOwner(sender));
        
        // get the current balance of this contract for the base asset
        let amount = this_balance(AssetId::base());
 
        // require the contract balance to be more than 0
        require(amount > 0, InvalidError::NotEnoughTokens(amount));
        
        // send the amount to the owner
        transfer(owner.unwrap(), AssetId::base(), amount);
    }
 
    #[storage(read)]
    fn get_count() -> u64 {
        return storage.item_counter.try_read().unwrap();
    }
}
```

## 建立合同
以下是您的说明的精美版本：

要格式化合同，请执行以下命令：

```sway
forc fmt
```

若要编译合约，请进入到合约文件夹并运行：

```sway
forc build
```

祝贺！您已在 Sway 中成功编写了完整的合同！

编译后，系统会自动生成abi.json, storage_slots.json和contract.bin.您可以在以下目录中找到这些文件：

```sway
contract/out/debug/*
```

## 部署协定
有关部署此合约的详细步骤，请参阅官方 Fuel 开发者计数器 dapp 指南： 
部署合约

要部署，如果您已经设置了 forc-wallet 并且您的账户中有测试网资金，请使用以下命令。

```sway
forc deploy --testnet
```


部署后，你将能够看到 contract/out/deployments 文件夹。前端集成的时候需要它。
