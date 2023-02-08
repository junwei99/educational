### Backend

output is unchanged, only input is changed

1. Controller

   method: POST & use @RequestBody

   ```java
   //make sure its POST
   public Result controller(@RequestBody List<String> cgisaiList, List<String> enodebId){

        CombinedDo combinedDOList = service(cgisaiList, enodebIdList)

        return Result.isOk(combinedDO)
   }
   ```

2. Services

   return value is the same, but the parameter is different

   ```java
   public CombinedDo service(List<String> cgisaiList, List<String> enodebIdList){

       List<DetailDO> ep = dataMapper.getEP(cgisaiList)
       List<FMTableDO> fm = dataMapper.getFM(cgisaiList)
       List<ABTableDO> ab = dataMapper.getAB(cgisaiList)
       List<CDTableDO> cd = dataMapper.getCD(enodebIdList)

       CombinedDo combinedDO = new CombinedDO(ep, fm, ab, cd)

       return combinedDO
   }
   ```

3. XML

   get cgiList and return list of DetailDO/FMTableDO/ABTableDO/CDTableDO

4. CombinedDO is unchanged

5. interfaces have to change (dataMapper, services, controller)

### Frontend

**Only come to frontend if u have tested with postman and backend works!!!**

1. AJAX POST

   - make sure when u call the api, u can see it on the network tab, if u can't then its frontend problem
   - make sure url is correct, test the same url on postman
   - console.log res.data, see if data is there or not
   - console.log the stringified cgisaiList, see if same as postman
   - **TIP**: use network tab, click on the api called, check "payload" (payload is requestBody AKA the json in postman AKA api input)
   - **TIP**: "preview" is the output of the api, response is the JSON version

```js
ajaxPost(
  url,
  JSON.stringify(cgisaiList),
  function (res) {
    console.log(res.data)
  },
  true
)
```

### Debugging

What happens when I get an error? learn to debug

1. use logger to log out the result
2. use breakpoint on debug mode, learn by watching youtube on intelliJ
