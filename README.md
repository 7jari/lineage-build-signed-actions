## What this does

Generates Android signing keys for LineageOS or its forks (such as crDroid) and pushes them to a private GitHub repository.

## Requirements

This workflow will only generate password-less keys. *This is due to building inline and GitHub Actions limitations*

*Works with LineageOS 19.1+ / crDroid 8.x+*

## Usage

- Fork this repository.
- Then, go to repository Settings > Secrets and Variables > Action > New repository secret; in name - `PAT` and in secret - paste your personal access token.
- Go to Actions tab, and if prompted, enable workflows.
- Specify an Android manifest repository link and its branch.
- Change the subject fields from their defaults, or not.
- Run the workflow.

After completion the keys are moved to `vendor/lineage-priv/keys` inside the Actions runner and a `keys.mk` file is written pointing `PRODUCT_DEFAULT_DEV_CERTIFICATE` at the releasekey.
Then, it will push the keys to a private GitHub repository on your account with the name `vendor_lineage-priv_keys`.

Clone the resulting repository to `vendor/lineage-priv/keys`, then build as usual.

If builds aren't being signed, add the following include to your device `.mk` file:

```makefile
-include vendor/lineage-priv/keys/keys.mk
```

## Notes

- You can get your personal access token in account Settings > Developer settings > Personal acccess token.
- The generated keys are your signing keys. DO NOT make your keys repository public!
- Make secure backups of your keys repository!

