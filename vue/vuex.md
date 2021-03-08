# vuex

有時候我們可能會需要在不同的`container` 上去使用同一個狀態\(state\)變數。因此`vuex` 將會完美的替我們解決。以下為其觀念圖

![](../.gitbook/assets/jie-tu-20210308-xia-wu-6.31.40.png)

## 開始教學

### 建立store

建立store，在`/src/store/` 下建立幾個檔案。

```javascript
// src/store/index.js
import { createStore } from 'vuex';
import createPersistedState from 'vuex-persistedstate';
import reducer from './vuexReducer';

import user from './modules/user';

export default createStore({
  state: {},
  mutations: {},
  actions: {},
  modules: {
    user,
  },
  plugins: [
    createPersistedState({
      key: 'VuexStorage',
      storage: window.localStorage,
      reducer,
    }),
  ],
});

```

```javascript
// src/store/vuexReducer.js
export default function (val) {
  return {
    user: val.user,
  };
}

```

```javascript
// src/store/modules/user.js
// ps: 建立資料夾modules，方便控管modules

const defaultState = {
  data: null,
};

const mutations = {
  setUserData(state, data) {
    state.data = data;
  },
  clearUserData(state) {
    state.data = null;
  },
  resetUserData(state, data) {
    state.data.name = data.name;
    state.data.email = data.email;
    state.data.position = data.position;
    state.data.place = data.place;
    state.data.public_contact = data.public_contact;
  },
  resetKeywords(state, keywords) {
    state.data.keywords = keywords;
  },
};

const actions = {
  login({ commit }, data) {
    commit('setUserData', data);
  },
  logout({ commit }) {
    commit('clearUserData');
  },
  reset({ commit }, data) {
    commit('resetUserData', data);
  },
  refreshKeywords({ commit }, keywords) {
    commit('resetKeywords', keywords);
  },
};

export default {
  namespaced: true,
  state: defaultState,
  actions,
  mutations,
};

```

### main.js引用

```javascript
// src/main.js
import { createApp } from 'vue';

import App from './App';
import router from './router';
import store from './store';

const app = createApp(App);

app.use(store).use(router).use(VueLazyLoad).mount('#app');

```

### 參考連結

* [官方連結](https://next.vuex.vuejs.org/)

