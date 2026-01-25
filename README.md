## What this does

Generates Android signing keys for crDroid and prepares them for inclusion in the build tree.

## Requirements

This script only works for password-less keys (DO NOT SET A PASSWORD)  
*This is due to building inline, other steps are necessary for a password*

*Works with crDroid 8.x+*

## Usage

Make the script executable and run it:

```bash
chmod +x create-signed-env.sh
./create-signed-env.sh
```

- You will be prompted for subject fields; press ENTER to accept defaults.
- The script prints the subject line and asks for confirmation before proceeding.
- Warning shown by the script: "Press ENTER TWICE to skip password (around 100 enter hits total). Cannot use a password for inline signing!" — follow the prompt if you want password-less keys.

After completion the keys are moved to `vendor/lineage-priv/keys` and a `keys.mk` file is written pointing `PRODUCT_DEFAULT_DEV_CERTIFICATE` at the releasekey.

If builds aren't being signed, add the following include to your device `.mk` file:

```makefile
-include vendor/lineage-priv/keys/keys.mk
```

## Important security note

- The generated keys are your signing keys. DO NOT publish them in a public repository.
- Make secure backups of `vendor/lineage-priv/keys`.

