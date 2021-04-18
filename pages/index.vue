<template>
  <div class="container">
    <div>
      <Logo />
      <h1 class="title">
        aws-kms-provider-browser-sandbox
      </h1>
      <div class="links">
        <a
          href="https://nuxtjs.org/"
          target="_blank"
          rel="noopener noreferrer"
          class="button--green"
        >
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          rel="noopener noreferrer"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import { KmsProvider } from "aws-kms-provider";
import Web3 from "web3";

async function sign() {
  const accessKeyId = "xxx";
  const secretAccessKey = "yyy";

  const region = "us-east-1";
  const keyId = "e9005048-475f-4767-9f2d-0d1fb0c89caf";
  const endpoint =
    "https://ropsten.infura.io/v3/bd35010d62134981a9e82dff4708728b";

  const provider = new KmsProvider(endpoint, {
    region,
    keyIds: [keyId],
    credential: {
      accessKeyId,
      secretAccessKey
    }
  });

  const web3 = new Web3(provider);

  const accounts = await web3.eth.getAccounts();

  const message = "poyo";
  const signature = await web3.eth.sign(message, accounts[0]);
  /*
  asyncToGenerator.js?1da1:6 Uncaught (in promise) TypeError: _constant__WEBPACK_IMPORTED_MODULE_2__.secp256k1N.sub(...).toBuffer is not a function
  が出るかも？
  */
  console.log({ signature });
}

export default Vue.extend({
  mounted() {
    sign();
  }
});
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
