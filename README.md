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
