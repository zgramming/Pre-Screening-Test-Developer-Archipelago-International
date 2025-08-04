# Pre Screening Test Developer

## Basic Question 

At least we should have 3 table to accomodire this scenario Roles,Users and Photos. Each table have these structure : 

**Role**
- id [varchar] (PK AI) 
- name [varchar]
- code [varchar] (unique)

**User**
- id [int] (PK AI)
- role_id [int] (FK)
- name [varchar]

**Photos**
- id [UUID] (PK)
- name
- status [enum] (pending, approve, reject)
- review_description (text)
- uploaded_by
- uploaded_at
- reviewed_by
- reviewed_at

With those structure we have, we already accomodire user can upload multiple photo and reviewed. So for the logic, this is pseudo code : 

1. User choose photos to be upload to server
2. Our backend will validate the photos to make sure it passed our validation like mimetype and size
3. If photos passed validation, it will inserted into Photos table we have created before
4. On reviewer side, only photos with status pending will be show and status can be updated into approve or reject. If photos rejected, reviewer can fill the information why photos rejected.
5. In user side, we can show the photos uploaded with the status (pending, approve and reject).

## Database Question

**1.**
```sql
SELECT COUNT(*) as Total FROM Customers where Country = 'Germany';
```

**2.**
```sql
SELECT COUNT(CustomerID), c.Country as Total FROM Customers c 
group by c.Country
having count(c.Country) > 4
order by count(c.Country) desc;
```

**3.**
```sql
select c.CustomerName, count(o.OrderID) as OrderCount, FORMAT(MIN(o.OrderDate), 'YYYY-mm-dd') as FirstOrder, FORMAT(MAX(o.OrderDate),'YYYY-mm-dd') as LastOrder from Customers as c
INNER JOIN Orders as o on (o.CustomerID = c.CustomerID)
group by c.CustomerName
having count(o.OrderID) > 4
order by MAX(o.OrderDate) desc
```

## Javascript/Typescript Questions

**1. Level 1**
```javascript
const titleCase = (value) => {
  const splits = value.split(" ").map((x) => x.toLowerCase());
  const result = [];
  for (const word of splits) {
    let mappingWord = "";
    for (let i = 0; i < word.length; i++) {
      const c = word[i];
      if (i == 0) {
        mappingWord += c.toUpperCase();
      } else {
        mappingWord += c;
      }
    }

    result.push(mappingWord);
  }

  return result.join(" ");
};

console.log(titleCase("I'm a little tea pot"));
console.log(titleCase("sHoRt AnD sToUt"));
console.log(titleCase("SHORT AND STOUT"));

const countWord = (value) => {
  let obj = {};
  const split = value
    .split(" ")
    .filter((x) => x != "")
    .map((x) => x.toLowerCase().trim().replaceAll(".").replaceAll(","));

  for (const number of split) {
    const existsNumber = obj[number];
    if (!existsNumber) {
      obj[number] = 1;
    } else {
      obj[number] += 1;
    }
  }

  const entries = Object.entries(obj);
  const sortedEntries = entries.sort((a, b) => a[1] - b[1]);
  return sortedEntries;
};

for (const [k, v] of countWord(
  "Four One two two three Three three four  four   four"
)) {
  console.log(${k} => ${v});
}
```

**2. Level 2**
```javascript
const delay = (delay) => {
  return new Promise((resolve) => resolve(setTimeout(resolve, delay)));
};

delay(3000).then((val) => console.log("test"));
```

**3. Level 2.5**
```javascript
async function fetchData(url) {
  return new Promise((resolve, reject) => {
    if (url) {
      return resolve(Data from ${url});
    }

    throw reject("URL is required");
  });
}

async function execute() {
  try {
    const data = await fetchData("https://example.com");
    console.log(Processed Data: ${data});
  } catch (e) {
    console.log(Process Error: ${e});
  }
}

execute();
```

## VUE.JS

## Website Security Best Practices

This is common security website vulnerabilities :

**1. CSRF**  
To handling this error, in .NET  we can add [ValidateAntiForgeryToken] in controller. We can use method JWT Authentication too if needed

**2. SQL Injection**  
To handling this error, in .NET we can use built in ORM EntityFramework. In EntityFramework the default already protected SQL Injection

**3. XSS**  
To handling this error, before data inserted into database we should validate and filter the input. If already inserted in razor page already handling it.

**4. DDOS Attack**  
To handling this error, we can set rate limiter middleware on the endpoint we want.

## Website Performance Best Practises

1. Caching response from server
2. Image optimize like mimetype webp, compress image
3. Use CDN to access file like css, image etc

## Golang (if interviewing for a Golang job) / .NET Candidate

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

public class Program
{
    public static void Main()
    {
        var result = Solutions.CountWord("Four, One two two three Three three four  four   four");

        foreach (var r in result)
        {
            Console.WriteLine($"{r.Key} => {r.Value}");
        }
    }
}

public class Solutions
{
    public static Dictionary<string, int> CountWord(string str)
    {
        Dictionary<string, int> obj = [];

        var filtered = str.Split(" ")
        .Select(x => x.ToLower().Trim().Replace(",", ""))
        .Where(x => x != "")
        .ToList();

        foreach (var word in filtered)
        {
            var isExist = obj.ContainsKey(word);
            if (isExist)
            {
                obj[word] += 1;
            }
            else
            {
                obj[word] = 1;
            }
        }

        return obj.OrderBy(x => x.Value).ToDictionary();
    }
}
```

## Tools (Rate yourself 1 to 5)

1. Git => 4
2. Redis => 3
3. VSCode / Jetbrains => 4
4. Linux => 4
5. AWS
    - EC2 => 2
    - Lambda => 2
    - RDS => 2
    - Cloudwatch => 2
    - S3 => 4
6. Unit Testing => 3
7. Kanban boards => 4
