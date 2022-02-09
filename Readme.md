# Solidity 0.8.11 教學

## pragma
- solidity
    - 運行版本
```solidity
pragma solidity ^0.8.11;
```

## contract
- is
    - 繼承
```solidity
contract Coin is ERC20 {}
```

## function
```solidity
function name() <visibility> <pure | view> <virtual> <override> <modifier()> returns () {}
```

- Visibility
    - private
        - 僅宣告當下的合約能讀取
    - public
        - 所有合約都能讀取
    - internal
        - 僅宣告當下、繼承該宣告合約能讀取
    - external
        - 僅外部合約可以讀取 (this 可以呼叫？)

- pure, view (節省 gas)
    - pure
        - 不讀不寫
    - view
        - 只讀不寫

- virtual
    - 允許繼承

- override
    - 覆蓋父層同名函式

- modifier
    - 共用邏輯統一包裝
        - _ 代表正常函式執行流程
    ```solidity
    modifier name(type param) {
        ...do something logical validation
        _;
    }
    ```

- returns
    - 定義回傳格式、參數數量
    ```solidity
    function name() returns (type param) {
        type param = 10;
    }
    ```
    ```solidity
    function name() returns (type) {
        type param = 10;

        return param;
    }
    ```

## 邏輯檢查
- require
    - 符合條件才會通過，還原狀態並返還剩餘 gas
```solidity
require(<logic>, "錯誤提示")
```

- revert
    - 還原狀態並返還剩餘 gas
```solidity
revert("錯誤提示")
```

- assert
    - 還原狀態燃燒所有剩餘 gas，常用於嚴重且不應該使用的邊界條件，不推薦使用 (為何不推薦？)
```solidity
assert(<logic>);
```

## type
- 沒有浮點數
- int
    - 有符號整數
    - 8, 16, 24, 32, 64, 128, 256
```
int8, int16, int32, int64, int128, int256
```

- uint
    - 無符號整數
    - 8, 16, 24, 32, 64, 128, 256
```
uint8, uint16, uint32, uint64, uint128, uint256
```

- string
    - 字串
    - 字串比對無法直接使用 == (為何有這種問題？)
```solidity
// method 1
sha3(str1) == sha3(str2);

// method 2
keccak256(bytes(str1)) == keccak256(bytes(str2));
```

- mapping
    - hash map
    - 若要遍歷則 key 需要自行儲存
```solidity
mapping(address => type) public param;
```

- bool
    - true, false

- address
    - 帳戶、合約位址

- enum
    - 限制參數值在一組變數中
```solidity
enum param {var1, var2, var3};
```

- bytes
    - (用途？)
    - 1, 2, 3, ..., 32

- struct
```solidity
struct NAME {
    type var1,
    type var2,
    ...
};
Name name({var1: "1", var2: "2"});
Name name("1", "2");
```

- array
    - 固定陣列
    ```solidity
    uint[5] arr;
    ```

    - 動態陣列
    ```solidity
    uint[] arr;
    ```

    - 記憶體陣列 (用途？)
    ```solidity
    uint[] memory arr = new uint[](5);
    ```

## super
## if else
- 沒有 switch
## for while do...while
## event emit indexed
## fallback function
## send transfer call
## payable
