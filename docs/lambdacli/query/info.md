# lambdacli query info

## Introduction

query the information of upgrade module

## Usage

```
lambdacli query info [flags]
```

Print query tendermint-validator-set flags:
```
lambdacli query info --help
```

## Examples
```
./lambdacli query info
```

output

```json
{
  "current_version": {
    "version": "0",
    "height": "0",
    "software": "0.4.8-goleveldb-release"
  },
  "upgrade_in_progress": {
    "version": "0",
    "height": "0",
    "software": ""
  }
}
```

