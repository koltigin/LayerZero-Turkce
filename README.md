# LayerZero - Omnichain Birlikte Çalışabilirlik Protokolü

Bu depo, LayerZero Endpoints için akıllı sözleşmeleri içerir. LayerZero'nun üzerinde inşa etmek isteyen geliştiriciler için lütfen [belgelere](https://layerzero.gitbook.io/docs/) bakın.

## Genel Bakış
LayerZero, zincirler arasında hafif ileti aktarımı için tasarlanmış bir Omnichain Birlikte Çalışabilirlik Protokolüdür. LayerZero, yapılandırılabilir güvenilmezlik ile özgün ve garantili mesaj teslimi sağlar. Protokol, GAS açısından verimli, yükseltilemeyen bir dizi akıllı sözleşme olarak uygulanmaktadır.

## Geliştirme
### Arayüzler
Bunu package.json dosyanıza ekleyin.

`
    "@layerzerolabs/contracts": "latest",
`
### Kurulum
- .env.example dosyasını .env dosyası olarak kopyalayın ve değişkenleri ekleyin.
- `yarn install`
### Test Etme
`yarn test`
#### Tek Test Dosyası
`yarn test test/Endpoint.test.js`
### Gas Kullanımı
`yarn test:gas`
### Kapsam
`yarn test:coverage`
### Lint
`yarn lint`

yalnızca lintleri içeren .js/.ts dosyaları

## Dağıtım

Dağıtım ağları, etiketlere göre oluşturulur.

#### Hardhat
`yarn dev`

yerel ortamı harekete geçirir ve sözleşmeleri devreye alır

#### Geliştirme
```
hardhat --network rinkeby-testnet deploy
hardhat --network rinkeby-sandbox deploy
```

#### Üretim
```
hardhat --network ethereum deploy
```

### Yeni bir ağ ekleme
1. Ağ ile [hardhat config](hardhat.config.ts) güncelleme
   1. desteklenen hazırlama ortamları için [STAGING_MAP](utils/deploy.js) bölümüne bakın 
2. Ağ ile [endpoints.json](constants/endpoints.json) güncelleme
3. endpoints.json'daki anahtarın hardhat'taki ağ adıyla eşleştiğinden emin olun

Örnek: Tek Katmanlı Sıfır Ağ / One LayerZero Network
```
//hardhat.config.ts
ethereum: {
    url: `{rpc address}`,
    chainId: 1, //chainlist id
}

//endpoints.json
"production": {
   ...
   "ethereum": {
     "id": 1 //layerzero chain id
   }
}
```
Örnek: Aynı zincir üzerinde birden fazla LayerZero Ağı (expandNetwork kullanarak)
```
//hardhat.config.ts
...expandNetwork({
    ropsten: {
        url: `{rpc address}`,
        chainId: 3, //chainlist id
    }
}, ["testnet", "sandbox"]),

//endpoints.json
"development": {
   ...
   "ropsten": {
     "id": 4 //layerzero chain id
   }
}
```
### Teşekkür

LayerZero Endpoints'i oluşturan çekirdek geliştirme ekibine teşekkür ederiz: Ryan Zarick, Isaac Zhang, Caleb Banister, Carmen Cheng ve T. Riley Schwarz


### LİSANS
LayerZero için birincil lisans, Business Source License 1.1'dir (BUSL-1.1). bkz. [`LICENSE`](./LICENSE).
