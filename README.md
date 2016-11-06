#What is vhdcopy.sh?

vhdcopy.sh is Azure CLI script to copy blobs from one subscription to another subscription with minimal intervention. This script depends on [**Azure CLI**] (https://azure.microsoft.com/en-us/documentation/articles/xplat-cli-install/) and the awesome command-line JSON processor [**jq**] (https://stedolan.github.io/jq/).

#How to use vhdcopy.sh
Install Azure CLI and JQ and add the source and target subscriptions on your system by running the following command (once for each subscription) -

```bash
azure login
```

This will display a code that you need to copy and paste in your browser after opening the http://aka.ms/devicelogin URL. Do this for both the subscriptions.

Now, run the following command to display the subscription IDs for your subscriptions -

```bash
azure account list
```

Last thing you need is the URL of the blob you need to copy between the subscriptions. Easiest way to get that information is from the Azure portal.

Run the script with the following syntax -

```bash
./vhdcopy.sh <source subscription id> <target subscription id> <URL of the blob you want to copy> <option-target storage account name> <optional-target container name>
```

Do this for every blob you need to copy and that's all - sit back and relax!

**Note**: This script was developed on a **Windows 10** system with **Bash on Ubuntu** running on it so I had to use sudo with every Azure CLI command - if you are on a Mac or Linux machine, you may not have to use sudo at all.

#How does this work?

This script use the Azure CLI commands along with the JQ command line tools to do the following -

1. Determine the resource group information for the source and target storage accounts
2. Create a storage account the target subscription. If no storage account was provided on the command line, it creates a new storage account with a prefix to the name of the storage account in the source subscription - **new**. A resource group is also created in the target subscription in the same manner. The location of these resources is set to same as the location information in the source subscription.
3. Determine if the source container/blob exists
4. Verify the presence of target container and create if not already present
5. Finally, copy the blob to the target subscription

**Disclaimer**: This script is provided as is and suitability for any purpose is not guaranteed - please test it thoroughly and modify as per your requirements.