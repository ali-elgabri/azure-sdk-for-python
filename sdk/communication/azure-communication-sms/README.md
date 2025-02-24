[![Build Status](https://dev.azure.com/azure-sdk/public/_apis/build/status/azure-sdk-for-python.client?branchName=master)](https://dev.azure.com/azure-sdk/public/_build/latest?definitionId=46?branchName=master)

# Azure Communication SMS Package client library for Python

This package contains a Python SDK for Azure Communication Services for SMS.
Read more about Azure Communication Services [here](https://docs.microsoft.com/azure/communication-services/overview)

[Source code](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/communication/azure-communication-sms) | [Package (Pypi)](https://pypi.org/project/azure-communication-sms/) | [API reference documentation](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/communication/azure-communication-sms) | [Product documentation](https://docs.microsoft.com/azure/communication-services/quickstarts/telephony-sms/send?pivots=programming-language-python)



## Getting started

### Prerequisites

- Python 2.7, or 3.6 or later is required to use this package.
- A deployed Communication Services resource. You can use the [Azure Portal](https://docs.microsoft.com/azure/communication-services/quickstarts/create-communication-resource?tabs=windows&pivots=platform-azp) or the [Azure PowerShell](https://docs.microsoft.com/powershell/module/az.communication/new-azcommunicationservice) to set it up.
- You must have a phone number configured that is associated with an Azure subscription

### Install the package

Install the Azure Communication SMS client library for Python with [pip](https://pypi.org/project/pip/):

```bash
pip install azure-communication-sms
```

## Key concepts

Azure Communication SMS package is used to do following:
- Send a 1:1 SMS Message
- Send a 1:N SMS Message

## Examples

The following section provides several code snippets covering some of the most common Azure Communication Services tasks, including:

- [Client Initialization](#client-initialization)
- [Send a 1:1 SMS Message](#send-a-1:1-sms-message)
- [Send a 1:N SMS Message](#send-a-1:n-sms-message)

### Client Initialization

To initialize the SMS Client, the connection string can be used to instantiate.
Alternatively, you can also use Active Directory authentication using DefaultAzureCredential.

```Python
from azure.communication.sms import SmsClient
from azure.identity import DefaultAzureCredential

connection_str = os.getenv('AZURE_COMMUNICATION_SERVICE_CONNECTION_STRING')
sms_client = SmsClient.from_connection_string(connection_string)
# To use Azure Active Directory Authentication (DefaultAzureCredential) make sure to have
# AZURE_TENANT_ID, AZURE_CLIENT_ID and AZURE_CLIENT_SECRET as env variables.
endpoint = os.getenv('AZURE_COMMUNICATION_SERVICE_ENDPOINT')
sms_client = SmsClient(endpoint, DefaultAzureCredential())
```

### Send a 1:1 SMS Message

Once the client is initialized, the `send` method can be invoked:

```Python
from azure.communication.sms import SendSmsOptions

sms_responses = sms_client.send(
    from_="<from-phone-number>",
    to="<to-phone-number-1>",
    message="Hello World via SMS",
    enable_delivery_report=True, # optional property
    tag="custom-tag") # optional property
```

- `from_`: An SMS enabled phone number associated with your communication service.
- `to`: The phone number or list of phone numbers you wish to send a message to.
- `message`: The message that you want to send.
- `enable_delivery_report`: An optional parameter that you can use to configure delivery reporting. This is useful for scenarios where you want to emit events when SMS messages are delivered.
- `tag`: An optional parameter that you can use to configure custom tagging.

### Send a 1:N SMS Message

Once the client is initialized, the `send` method can be invoked:

```Python
from azure.communication.sms import SendSmsOptions

sms_responses = sms_client.send(
    from_="<from-phone-number>",
    to=["<to-phone-number-1>", "<to-phone-number-2>", "<to-phone-number-3>"],
    message="Hello World via SMS",
    enable_delivery_report=True, # optional property
    tag="custom-tag") # optional property
```

- `from_`: An SMS enabled phone number associated with your communication service.
- `to`: The phone number or list of phone numbers you wish to send a message to.
- `message`: The message that you want to send.
- `enable_delivery_report`: An optional parameter that you can use to configure delivery reporting. This is useful for scenarios where you want to emit events when SMS messages are delivered.
- `tag`: An optional parameter that you can use to configure custom tagging.


## Troubleshooting
The Azure Communication Service SMS client will raise exceptions defined in [Azure Core](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/core/azure-core/README.md).

## Next steps
### More sample code

Please take a look at the [samples](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/communication/azure-communication-sms/samples) directory for detailed examples of how to use this library to send an sms.

## Provide Feedback

If you encounter any bugs or have suggestions, please file an issue in the [Issues](https://github.com/Azure/azure-sdk-for-python/issues) section of the project

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us the rights to use your contribution. For details, visit https://cla.microsoft.com.

When you submit a pull request, a CLA-bot will automatically determine whether you need to provide a CLA and decorate the
PR appropriately (e.g., label, comment). Simply follow the instructions provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

<!-- LINKS -->
[azure_core]: https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/core/azure-core/README.md