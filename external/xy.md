### \*\* **Please read through and try to understand first instead of copying one by one** \*\*

&nbsp;

### Backend

output is unchanged, only input is changed

1. #### Controller

   **previous GET API** :

   make a get request to `http://localhost/data/getEP?cgisai=12121&enodebId=121212)`

   **new POST API**:

   make a POST request to `http://localhost/data/getEP` with the request body (JSON) below :

   ```json
   {
     "cgisaiList": ["123abc", "456bcd"],
     "enodebIdList": ["123fao", "129nadf"]
   }
   ```

   we need to create a **new Class** for the input of the API aka controller :

   ```java
   //rename this class to something else more useful
   private class CombinedDOParam {
      List<String> cgisaiList = []
      List<String> enodebIdList = []

      //this is a constructor, its the same as the name of the class
      public combinedVO(List<String> cgisaiList, List<String> enodebIdList){
         this.cgisaiList = cigsaiList
         this.enodebIdList = enodebIdList
      }

      //u can put getters and setters below but its not needed for this feature
   }

   ```

   The class above will be the **type for the new JSON param** above (this is used as param for the api) :

   using the **class created above as the type of the parameter** for the controller function

   ```java
   // method: POST & use @RequestBody
   // param is the new object created using the class shown above
   public Result controller(@RequestBody CombinedDOParam combinedDOParam){

        CombinedDo combinedDO = service(combinedDOParam)

        return Result.isOk(combinedDO)
   }
   ```

2. Services

   return value is the same, but the parameter is different

   ```java
   public CombinedDo service(CombinedDOParam combinedDOParam){

      //get the cgisaiList and enodebIdList from the combinedDOParam object
      List<String> cgisaiList = combinedDOParam.cgisaiList
      List<String> enodebIdList = combinedDOParam.enodebIdList

      //pass to each dataMapper function to get data using SQL (XML file)
      List<DetailDO> ep = dataMapper.getEP(cgisaiList)
      List<FMTableDO> fm = dataMapper.getFM(cgisaiList)
      List<ABTableDO> ab = dataMapper.getAB(cgisaiList)
      List<CDTableDO> cd = dataMapper.getCD(enodebIdList)

      //once data is retrieved from each table, create new CombinedDO object
      CombinedDo combinedDO = new CombinedDO(ep, fm, ab, cd)

      return combinedDO
   }
   ```

3. XML

   input cgiList & enodebList and return list of DetailDO/FMTableDO/ABTableDO/CDTableDO

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

&nbsp;

```js
common.ajaxPost(
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
2. use breakpoint on debug mode, learn by watching youtube on intelliJ (important for backend)
