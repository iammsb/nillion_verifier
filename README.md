<h2 align=center>Nillion Verifier Node Guide</h2>

- You can use either VPS or Ubuntu on Windows
- Ubuntu troubleshooting related video is [here](https://x.com/ZunXBT/status/1827779868630876651)
- Make sure that you have a nillion address, if u have not, you can install [Keplr](https://chromewebstore.google.com/detail/keplr/dmkamcknogkgcdfhhbddcghachkejeap) and create a nillion address
- Now visit this [website](https://chains.keplr.app) and search `nillion` and add nillion testnet to your keplr wallet
- Open your Keplr wallet, search for `nillion` , u will get your nillion address
- Now request nillion faucet from [here](https://faucet.testnet.nillion.com/)
- Use this command to install docker on your system
```bash
sudo apt update -y && sudo apt install -y apt-transport-https ca-certificates curl software-properties-common && sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg && echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null && sudo apt update -y && apt-cache policy docker-ce && sudo apt install -y docker-ce && sudo usermod -aG docker ${USER} && su - ${USER} -c "groups" && docker --version
```
- Use this command to pull nillion accuser image
```bash
docker pull nillion/retailtoken-accuser:latest
```
- Use the below command to create a directory and to initialise the accuser
```bash
mkdir -p nillion/accuser && docker run -v ./nillion/accuser:/var/tmp nillion/retailtoken-accuser:latest initialise
```
- After executing the above command, you will see `accound_id` and `public_key` in your terminal, copy the value
- Now visit [this site](https://verifier.nillion.com/verifier), submit your `accound_id` and `public_key` in the appropriate field
- Visit [faucet site](https://faucet.testnet.nillion.com/) to request faucet in your `account_id` you copied earlier
- Now run this command to get your accuser wallet private key
```bash
cat ~/nillion/accuser/credentials.json
```
- Copy the private key and save it, if you lose, you will not regain access to your accuser wallet
---
<h2 align=center>NOW TAKE A BREAK FOR 60 MINS</h2>

---
- After 60 mins, run this final command
```bash
current_block=$(curl -s https://testnet-nillion-rpc.lavenderfive.com/abci_info | jq -r '.result.response.last_block_height'); block_start=$((current_block - 5)); docker run -v $(pwd)/nillion/accuser:/var/tmp nillion/retailtoken-accuser:latest accuse --rpc-endpoint "http://65.109.222.111:26657" --block-start $block_start
```
- Done ✅ , Follow me [iamMSB]([https://x.com/MichaelSethBasi])
