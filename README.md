# azure_servicebus_queue_devcontainer

Before testing or running the contained code you will need to do the following
- Create an azure resource group for the service bus
- Create a namespace for the azure service bus
- Create a queue to receive the service bus messages
- Retrieve the Primary Connection string from the RootManageSharedAccessKey under the shared access policies section for the azure service bus resourcce group

## Create an azure resource group for the service bus
### Use the azure cli to do the following
Replace <myLocation> with your closest azure region
```
myLocation=eastus
myNameSpaceName=az204svcbustopic$RANDOM
myResourceGroup=az204-svcbus-rg$RANDOM
myTopic=sciencereadings
mySubscription=scientists
```
```
az group create --name $myResourceGroup --location $myLocation
```
## Create a namespace for the azure service bus
```
az servicebus namespace create \
--resource-group $myResourceGroup \
--name $myNameSpaceName \
--location $myLocation
```
## Create a topic to receive the service bus messages
```
az servicebus topic create --resource-group $myResourceGroup \
--namespace-name $myNameSpaceName \
--name $myTopic
```
## Create a subscription to receive the service bus messages from topics
```
az servicebus topic subscription create --resource-group $myResourceGroup \
--namespace-name $myNameSpaceName \
--topic-name $myTopic \
--name $mySubscription
```
## Retrieve the Primary Connection string from the RootManageSharedAccessKey under the shared access policies section for the azure service bus resource group
- Open the Azure portal and navigate to the az204-svcbus-rg resource group.
- Select the az204svcbus resource you created.
- Select Shared access policies in the Settings section, then select the RootManageSharedAccessKey policy.
- Copy the Primary Connection String from the dialog box that opens up and save it to a file, or leave the portal open and copy the key when needed.