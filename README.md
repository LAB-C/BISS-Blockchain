# BISS-Blockchain

## Usage

### 0. Open node with ngrok
```bash
ngrok http -hostname=klaytn.ngrok.io 8551
```

running on http://klaytn.ngrok.io

### 1. `klaytn.py`를 쓰자~!
```python
from klaytn import *

klay = Klaytn('http://klaytn.ngrok.io')
```

프로젝트 폴더에는 (`caver-js`가 설치된)`node_modules`, `blockchain` 폴더와 `klaytn.py`, `send.js`가 있어야 한다.
 
새 파이썬 스크립트를 작성하고 위와 같이 config한다. `example.py`를 이용하면 쉽게 개발할 수 있다.

> 이건 진짜 꼭 필요한 것만 있는 파이썬 API야~!

### 2. 지갑을 생성하자.
```python
wallet = klay.newAccount('_labc')
```
패스프레이즈가 `_labc`인 새로운 어카운트를 만든다. 지갑을 생성할 때 자동으로 faucet를 돌려서 1000klay를 저장한다(gas 비용이 필요하므로).

`klay.newAccount()`는 지갑 주소를 반환한다.

### 3. 어카운트를 언락하자.
```python
klay.unlockAccount(wallet, '_labc', 30000))
```

패스프레이즈가 `_labc`인 wallet이라는 지갑주소를 언락한다. 마지막 인수는 언락 기간(초)이다. 즉 위 예제의 wallet은 30000초 동안 언락되고 그 이후에는 다시 lock된다.

### 4. 데이터를 보내자.
```python
print(klay.sendData(wallet, 'so what?'))
```

이런 식으로 송신자의 wallet과 보낼 data를 올리면 되는데 아마 data에 따옴표가 들어가면 제대로 안될 것 같다. 

> 공백은 상관없는 것 같은데 뭐 따옴표나 공백이 꼭 들어갈 필요는 없잖아? 만약 터지면 한대 때리고 고쳐줄 테니까 꼭 불러줘.

## How to deploy & test

### 1. Generate new account or use any account & Unlock
Change address in `./blockchain/truffle.js`, `./blockchain/truffle.js`

### 2. Deploy smart contract on network

```bash
$ cd blockchain
$ truffle deploy --network klaytn --reset
```

Get `Transmission` smart contract address from output

### 3. Modify `test.js`
Modify smart contract address and sender address in `test.js` and run with `node test.js`
