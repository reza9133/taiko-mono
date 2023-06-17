---
title: TaikoData
---

## TaikoData

### Config

```solidity
struct Config {
  uint256 chainId;
  uint256 maxNumProposedBlocks;
  uint256 blockRingBufferSize;
  uint256 maxVerificationsPerTx;
  uint64 blockMaxGasLimit;
  uint64 blockFeeBaseGas;
  uint64 maxTransactionsPerBlock;
  uint64 maxBytesPerTxList;
  uint256 txListCacheExpiry;
  uint256 proofCooldownPeriod;
  uint256 systemProofCooldownPeriod;
  uint256 ethDepositRingBufferSize;
  uint64 ethDepositMinCountPerBlock;
  uint64 ethDepositMaxCountPerBlock;
  uint96 ethDepositMaxAmount;
  uint96 ethDepositMinAmount;
  uint256 ethDepositGas;
  uint256 ethDepositMaxFee;
  bool relaySignalRoot;
}
```

### StateVariables

```solidity
struct StateVariables {
  uint48 feePerGas;
  uint64 genesisHeight;
  uint64 genesisTimestamp;
  uint64 numBlocks;
  uint64 lastVerifiedBlockId;
  uint64 nextEthDepositToProcess;
  uint64 numEthDeposits;
}
```

### BlockMetadataInput

```solidity
struct BlockMetadataInput {
  bytes32 txListHash;
  address beneficiary;
  uint32 gasLimit;
  uint24 txListByteStart;
  uint24 txListByteEnd;
  uint8 cacheTxListInfo;
}
```

### BlockMetadata

```solidity
struct BlockMetadata {
  uint64 id;
  uint64 timestamp;
  uint64 l1Height;
  bytes32 l1Hash;
  bytes32 mixHash;
  bytes32 txListHash;
  uint24 txListByteStart;
  uint24 txListByteEnd;
  uint32 gasLimit;
  address beneficiary;
  address treasury;
  struct TaikoData.EthDeposit[] depositsProcessed;
}
```

### BlockEvidence

```solidity
struct BlockEvidence {
  bytes32 metaHash;
  bytes32 parentHash;
  bytes32 blockHash;
  bytes32 signalRoot;
  bytes32 graffiti;
  address prover;
  uint32 parentGasUsed;
  uint32 gasUsed;
  uint16 verifierId;
  bytes proof;
}
```

### ForkChoice

```solidity
struct ForkChoice {
  bytes32 key;
  bytes32 blockHash;
  bytes32 signalRoot;
  uint64 provenAt;
  address prover;
  uint32 gasUsed;
}
```

### Block

```solidity
struct Block {
  mapping(uint256 => struct TaikoData.ForkChoice) forkChoices;
  bytes32 metaHash;
  uint64 blockId;
  uint64 proposedAt;
  uint48 feePerGas;
  uint32 gasLimit;
  uint24 nextForkChoiceId;
  uint24 verifiedForkChoiceId;
  address proposer;
  address prover;
  uint16 proofWindow;
}
```

### TxListInfo

```solidity
struct TxListInfo {
  uint64 validSince;
  uint24 size;
}
```

### EthDeposit

```solidity
struct EthDeposit {
  address recipient;
  uint96 amount;
  uint64 id;
}
```

### State

```solidity
struct State {
  mapping(uint256 => struct TaikoData.Block) blocks;
  mapping(uint256 => mapping(bytes32 => mapping(uint32 => uint256))) forkChoiceIds;
  mapping(bytes32 => struct TaikoData.TxListInfo) txListInfo;
  mapping(uint256 => uint256) ethDeposits;
  uint64 genesisHeight;
  uint64 genesisTimestamp;
  uint64 __reserved70;
  uint64 __reserved71;
  uint64 __reserved80;
  uint64 numEthDeposits;
  uint64 numBlocks;
  uint64 nextEthDepositToProcess;
  uint64 lastVerifiedAt;
  uint64 lastVerifiedBlockId;
  uint48 feePerGas;
  uint16 avgProofDelay;
  uint64 __reserved90;
  uint256[42] __gap;
}
```
