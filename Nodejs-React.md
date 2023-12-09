
Nodejs 18 indirmek için:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install curl
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```

sonra nodejs kurmaya başlayabilirsin:

```
sudo apt-get install nodejs
```

sürümü kontrol et:

```
node -v
npm -v
```

şimdi proje oluşturmak için:

```
mkdir Gokmen
cd Gokmen
npm init
```
Aynı dosyanın içerisinde şimdi:

```
npx create-react-app gokmen-app
cd gokmen-app
npm install socket.io
npm install express
```


App.js kodlarını düzenledikten sonra başlatmak için:

```
npm start
```
