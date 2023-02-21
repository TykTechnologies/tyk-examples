# Examples Repository

This repository contains examples that can be imported into Tyk Gateway or Tyk Dashboard.
This can be done either by using [tyk-sync](https://github.com/TykTechnologies/tyk-sync) as CLI or by manually copying the API/Policy Definitions.

## Importing examples
In terms of importing examples `tyk-sync` will be the easier options to get started quickly. 
The manual approach on the other hand will allow you to pick the parts of the examples that you need.
Either way is fine.

### Using `tyk-sync`
> Before starting with `tyk-sync` please make sure that you have followed the [prerequisites](https://github.com/TykTechnologies/tyk-sync#prerequisites) for using `tyk-sync`.
> Also please refer to the `tyk-sync` [documentation](https://tyk.io/docs/tyk-sync/) for more details.

#### Get an overview of all examples
The following command will print a list of all available examples in this repository:
```
tyk-sync examples
```

#### Get more details of an example
To see more details of an example like the features that are being used or the minimal Tyk version use this command:
```
tyk-sync examples show --location="[location]"
```
> Location can be found in the examples overview.

#### Import an example
To import an example directly into the Dashboard you can use this command:
```
tyk-sync examples publish -d="[dashboard_url]" -s="[secret]" -l="[location]"
```
> Location can be found in the examples overview.\
> Secret can be found in your Dashboard profile. \
> Dashboard URL is the root URL of your Dashboard

### Manual import

#### For Dashboard
Go to **APIs > Import API** and select **Tyk API**. There you can paste the API Definition. 

You can also use the Dashboard API - [please refer to the documentation on how to use it](https://tyk.io/docs/getting-started/import-apis/).

#### For Gateway (Open-Source)
Place the API definition inside the `apps` folder.

## How this repository works
All examples are placed in subfolders.

The root contains a `repository.json` which serves as an index file for the examples and is basically the source of truth.
You can programmatically read this file if you want to automate the import of examples - that's how `tyk-sync` works.

The `repository.schema.json` contains the JSON schema for the index file and can be used to validate it.

## Something doesn't work?
Please let us know if an example doesn't work. For that you can create an issue and tell us about the problem - but before doing it 
please make sure that your Tyk version aligns with the `MinTykVersion` of an example.