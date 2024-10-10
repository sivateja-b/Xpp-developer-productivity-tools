**This tool helps you easily create X++ data contract classes based on your technical requirements. Whether you need a contract based on a JSON structure, a class for a SysOperation framework batch job, an SSRS report, or a custom service in Finance and Operations, this tool has you covered!**

****Note:** *Query-based contract data members are not supported by this generator yet.***
### **Control Descriptions:**

-   **Class Name**: Enter the name of the class you want to create.
-   **Type**: Specify the EDT name or primitive type for the data member.
-   **Variable Name**: Enter the variable name of the data member.
-   **Collection Type**: If the data type is a List, specify the collection type from the AX Types enumerator.
-   **Collection Contract Name**: If the collection type is a Class, specify the contract type for each individual element.
-   **Generate Button**: Creates the X++ contract class based on your inputs.
-   **Result Box**: Displays the generated X++ contract class code, ready for you to copy and use in development.

**Example**


The JSON:
```
{
  "user":"Teja",
  "addresses":[{"addressName":"DLV","text":"Delivery"},{"addressName":"Ofc","text":"Office"}],
  "numbers":[1,2,4,5]
}
```


Identify sub contract:
"addresses":[{"addressName":"DLV","text":"Delivery"},{"addressName":"Ofc","text":"Office"}]

Create contract for this subcontract:
Inputs in the tool are as follows -
![image](https://github.com/sivateja-b/Xpp-developer-productivity-tools/assets/63949792/d1f3ff58-ebd6-4ef0-b07d-31400ff79006)

```
[DataContract("addresses")]
public class Addresses
{
    str addressName;
    str text;

    [DataMember("addressName")]
    public str parmAddressName(str _addressName = addressName)
    {
        addressName = _addressName;
        return addressName;
    }

    [DataMember("text")]
    public str parmText(str _text = text)
    {
        text = _text;
        return text;
    }

}
```
Once all subcontracts are created create the root contract:
Inputs in the tool are as follows -
![image](https://github.com/sivateja-b/Xpp-developer-productivity-tools/assets/63949792/af62f81a-c3dd-4d7f-8117-3f6c61c5aa96)

```
[DataContract("UserResponse")]
public class UserResponse
{
    str user;
    List addresses;
    List numbers;

    [DataMember("user")]
    public str parmUser(str _user = user)
    {
        user = _user;
        return user;
    }

    [DataMember("addresses"),DataCollection(Types::Class,classStr(Addresses))]
    public List parmAddresses(List _addresses = addresses)
    {
        addresses = _addresses;
        return addresses;
    }

    [DataMember("numbers"),DataCollection(Types::Integer)]
    public List parmNumbers(List _numbers = numbers)
    {
        numbers = _numbers;
        return numbers;
    }

}
```
