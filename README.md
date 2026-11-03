> [!WARNING]
> **Deprecated.** `<become-reverification-button>` is no longer maintained.
>
> **Use this instead:** [Become Web Button documentation](https://github.com/Becomedigital/Become-web-button). Re-verification is now part of the Become Button and the Become KYC SDK: set `flow="reverification"`.

## Migrate in 2 steps

**1. Replace the script**

```html
<!-- Before -->
<script src="https://onboarding.svi.becomedigital.net/resources/reverification-button.js"></script>

<!-- After -->
<script src="https://websdk.svi.becomedigital.net/sdk/become-web-button.js"></script>
```

**2. Replace the tag and add `flow="reverification"`**

```html
<!-- Before -->
<become-reverification-button
  userId="<YOUR_USER_ID>"
  contractId="<YOUR_CONTRACT_ID>"
  token="<YOUR_JWT_TOKEN>"
/>

<!-- After -->
<become-button
  flow="reverification"
  user-id="<YOUR_USER_ID>"
  contract-id="<YOUR_CONTRACT_ID>"
  access-token="<YOUR_JWT_TOKEN>"
></become-button>
```

`user-id` is required for re-verification. The previous names (`userId`, `contractId`, `token`) are also accepted.

**Events**

| Before | After |
|--------|-------|
| `become:result` | `become:result`. The result is in `event.detail.data` |
| `become:userFinishedSdk` | `become:userFinishedSdk` |
| `become:exitedSdk` | `become:exitedSdk` |
| `become:sdkLoaded`, `become:verificationStarted` | Not available |
| | `become:errorSdk`: emitted when the verification cannot start or fails |

```js
const button = document.querySelector('become-button');

button.addEventListener('become:result', ({ detail }) => {
  console.log('Re-verification result:', detail.data);
});

button.addEventListener('become:errorSdk', ({ detail }) => {
  console.error('Re-verification error:', detail.code, detail.message);
});
```

See the [Become Web Button documentation](https://github.com/Becomedigital/Become-web-button) for every attribute, event and payload.

---

Already using `<become-reverification-button>`? It keeps working, so you can migrate at your own pace. The previous documentation is in this repository's [history](<LINK_TO_LAST_COMMIT_OR_TAG>).
