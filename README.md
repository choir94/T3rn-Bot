
# Bot T3rn Auto Bridge

### Join Channel Telegram Airdrop Node
--  https://t.me/airdrop_node

## Install Node.js dan Npm
```
sudo apt-get install nodejs npm -y
sudo npm install n -g
sudo n latest
```
### Buat Directory baru
```
mkdir t3rn-auto
cd t3rn-auto
npm init
npm install ethers@5
```
### Buat/edit file index.js
```
nano index.js
```
### Copy paste ke index js
```
const { BigNumber } = require("ethers"); const { parseEther, formatEther } = require("ethers/lib/utils"); const ethers = require('ethers') const sleepTimer = () => { return Math.random() * (120000 - 60000) + 60000; } function generateRandomAmount() { return parseFloat(Math.random() * (0.0200 - 0.0100) + 0.0100).toFixed(4); } function getRandomElement() { let chainList = ["2737370","f707370","26c7373","1726274"] const randomIndex = Math.floor(Math.random() * chainList.length); return chainList[randomIndex]; } function getSourceNetwork() { const sourceConfigList = [{ name: "base-sepolia", chainId: "84532", address: "0x30A0155082629940d4bd9Cd41D6EF90876a0F1b5", provider: "https://base-sepolia.blockpi.network/v1/rpc/public", bridgeId: "2737370" },{ name: "blast-sepolia", chainId: "168587773", address: "0x1D5FD4ed9bDdCCF5A74718B556E9d15743cB26A2", provider: "https://blast-sepolia.blockpi.network/v1/rpc/public", bridgeId: "26c7373" },{ name: "op-sepolia", chainId: "11155420", address: "0xF221750e52aA080835d2957F2Eed0d5d7dDD8C38", provider: "https://optimism-sepolia.blockpi.network/v1/rpc/public", bridgeId: "f707370" },{ name: "arb-sepolia", chainId: "421614", address: "0x8D86c3573928CE125f9b2df59918c383aa2B514D", provider: "https://arbitrum-sepolia.blockpi.network/v1/rpc/public", bridgeId: "1726274" }] const randomIndex = Math.floor(Math.random() * sourceConfigList.length); return sourceConfigList[randomIndex]; } const bridge = async (privateKey) => { console.log("=========================================") let config = getSourceNetwork() let arbProvider = config.provider const providerJSON = new ethers.providers.JsonRpcProvider(arbProvider); const wallet = new ethers.Wallet(privateKey, providerJSON) const balance = await providerJSON.getBalance(wallet.address).catch((e) => 0) console.log(`loaded wallet ${config.name}, balance: ${formatEther(balance)} ETH`) let addrBridge = config.address let amountBridge = parseEther(generateRandomAmount()) console.log(`bridge amount ${formatEther(amountBridge)} ETH`) let netAmountBridge = amountBridge - (amountBridge * 0.01) console.log(`net amount ${formatEther(netAmountBridge.toString())}`) let chainId = getRandomElement() console.log(`bridge from ${config.name} to ${chainId}`) // Translated message if (chainId == config.bridgeId) { console.log(`[x] Destination Chain Cannot Be the Same as Source Chain, Try Again`) return bridge(privateKey) } // Translated message if (balance.lt(amountBridge)) { console.log(`[x] Insufficient Balance to Bridge, Try Again`) return bridge(privateKey) } let dataBridge = `0x56591d596${chainId}000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000${wallet.address.slice(2).toLowerCase()}00000000000000000000000000000000000000000000000000${BigNumber.from(netAmountBridge.toString())._hex.slice(2)}0000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000${BigNumber.from(amountBridge.toString())._hex.slice(2)}` let txEstimateGas = await wallet.estimateGas({ to: addrBridge, value: amountBridge, data: dataBridge }).catch((e) => ({status: 500, message: e.reason})) if (BigNumber.isBigNumber(txEstimateGas)) { let txSend = await wallet.sendTransaction({ to: addrBridge, value: amountBridge, data: dataBridge }).catch((e) => ({status: 500, message: e.reason, hash: null})) console.log(`√ Tx Bridge: ${txSend.hash}`) return setTimeout(() => { bridge(privateKey) }, sleepTimer()) } else { console.log(txEstimateGas) return setTimeout(() => { bridge(privateKey) }, sleepTimer()) } } bridge("0x00000") // -> CHANGE YOUR PRIVATE KEY
```
Edit privat key dalam  bridge("0x00000")

### Start Running
```
node index.js
```

### Join Channel Telegram Airdrop Node
--  https://t.me/airdrop_node

