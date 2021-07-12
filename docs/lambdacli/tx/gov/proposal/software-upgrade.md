# lambdacli tx gov submit-proposal software-upgrade

## Description

Submit a software upgrade proposal along with an initial deposit

## Usage

```
lambdacli tx gov submit-proposal software-upgrade <path/to/proposal.json> <flags>
```

Print help messages:

```
lambdacli tx gov submit-proposal software-upgrade -h
```

## Examples
```$xslt
 ./lambdacli tx gov submit-proposal software-upgrade ../upgrade.json --from master --broadcast-mode block
{"chain_id":"testing","account_number":"0","sequence":"6","fee":{"amount":null,"gas":"200000"},"msgs":[{"type":"cosmos-sdk/MsgSubmitProposal","value":{"content":{"type":"lambda/SoftwareUpgradeProposal","value":{"title":"Software Upgrade","description":"Upgrade to new version","version":"1","software":"https://github.com/LambdaIM/launch/releases/tag/v0.3.4","switch_height":"50","threshold":"0.800000000000000000"}},"initial_deposit":[{"denom":"ulamb","amount":"520000000"}],"proposer":"lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym"}}],"memo":""}

confirm transaction before signing and broadcasting [Y/n]: y
Password to sign with 'master':
Response:
  Height: 53
  TxHash: 92628C823803BC1D52287B38624A4C06814996A48C4DF1D4DA3AFEFF9F1C6F62
  Data: 0102
  Raw Log: [{"msg_index":"0","success":true,"log":""}]
  Logs: [{"msg_index":0,"success":true,"log":""}]
  GasWanted: 200000
  GasUsed: 69989
  Tags:
    - action = submit_proposal
    - sender = lambda105jf3p5qkrnq973xmc6e9f8asly79sv7phcrym
    - proposal_id = 2
```

`upgrade.json` file looks like this
```json
{
	"title": "Software Upgrade",
	"description": "Upgrade to new version",
	"version": "1",
	"software": "https://github.com/LambdaIM/launch/releases/tag/v0.3.4",
	"switch_height": "50",
	"threshold": "0.8",
	"deposit": [{
		"denom": "ulamb",
		"amount": "520000000"
	}]
}
```
**note**

`switch_height` must greater than current chain lastest height and  `version` must greater than current version.
If not even the proposal passed and the chain will not switch to new version