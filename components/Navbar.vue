<template>
  <b-navbar wrapper-class="container" class="header">
    <template slot="brand">
      <b-navbar-item tag="router-link" to="/" active-class="">
        <Logo />
      </b-navbar-item>
    </template>
    <template slot="start">
      <b-navbar-item
        href="https://medium.com/@tornado.cash/tornado-cash-governance-proposal-a55c5c7d0703"
        target="_blank"
        class="decorate"
      >
        {{ $t('info') }}
      </b-navbar-item>
    </template>
    <template slot="end">
      <b-navbar-item tag="div">
        <div class="buttons">
          <b-button
            v-if="isLoggedIn"
            type="is-primary"
            outlined
            icon-left="logout"
            @click="onLogOut"
            >{{ $t('logout') }}</b-button
          >
          <b-button
            v-else
            type="is-primary"
            outlined
            icon-left="wallet"
            @click="onLogIn"
            >{{ $t('connect') }}</b-button
          >
        </div>
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script>
import Logo from '@/components/Logo'
import Web3Connect from '@/components/Web3Connect'
import { mapGetters, mapActions } from 'vuex'

export default {
  components: {
    Logo,
  },
  computed: {
    ...mapGetters('provider', ['getProviderName']),
    isLoggedIn() {
      return !!this.getProviderName
    },
  },
  methods: {
    ...mapActions('provider', ['clearState']),
    onLogIn() {
      this.$buefy.modal.open({
        parent: this,
        component: Web3Connect,
        hasModalCard: true,
        width: 440,
      })
    },
    onLogOut() {
      this.clearState()
    },
  },
}
</script>
