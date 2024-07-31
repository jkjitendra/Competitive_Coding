# REST API: CountryCodes

## Problem Statement

Given a country name and a phone number, query the API at *https://jsonmock.hackerrank.com/api/countries?name=country* to get the country's calling codes. If there are multiple calling codes, use the one at the highest index. Prepend the calling code to the phone number and return the string. If the data array is empty, return the string -1.

The format of the number should be:

+`<Calling Code>`space>`<Phone Number>`

**Example:**

`+1 765355443`

The response is a JSON object with 5 fields. The essential field is data:

* ﻿﻿data: Either an empty array or an array with a single object that contains the country's record.
* ﻿﻿In the data array, the country has the following schema:
  - name: The name of the country (String)
  - callingCodes. An array of the country's calling codes (String Array)
  - A number of fields that are not of interest.

page, per_page, total, total_pages, etc., are not required for this task.

If the country is found, the data array contains exactly 1 element. If not, it is empty, and the function should return '-1':

If the country name is 'Afghanistan', for example, query [https://jsonmock.hackerrank.com/api/countries?name=Afghanistan.](https://jsonmock.hackerrank.com/api/countries?name=Afghanistan) A portion of the country record for Afghanistan is:

```
{
  "page": 1,
  "per_page": 10,
  "total": 1,
  "total_pages": 1,
  "data": [
    {
      "name": "Afghanistan",
      "nativeName": "افغانستان",
      "topLevelDomain": [
        ".af"
      ],
      "alpha2Code": "AF",
      "numericCode": "004",
      "alpha3Code": "AFG",
      "currencies": [
        "AFN"
      ],
      "callingCodes": [
        "93"
      ],
      "capital": "Kabul",
      "altSpellings": [
        "AF",
        "Afġānistān"
      ],
      "relevance": "0",
      "region": "Asia",
      "subregion": "Southern Asia",
      "language": [
        "Pashto",
        "Dari"
      ],
      "languages": [
        "ps",
        "uz",
        "tk"
      ],
      "translations": {
        "de": "Afghanistan",
        "es": "Afganistán",
        "fr": "Afghanistan",
        "it": "Afghanistan",
        "ja": "アフガニスタン",
        "nl": "Afghanistan",
        "hr": "Afganistan"
      },
      "population": 26023100,
      "latlng": [33, 65],
      "demonym": "Afghan",
      "borders": [
        "IRN",
        "PAK",
        "TKM",
        "UZB",
        "TJK",
        "CHN"
      ],
      "area": 652230,
      "gini": 27.8,
      "timezones": [
        "UTC+04:30"
      ]
    }
  ]
}
```

**Function Description**
Complete the getPhoneNumbers function in the editor.

*getPhoneNumbers* has the following parameters:

string country: the country to query
string phoneNumber: the phone number

**Returns**

string: the completed phone number or "-1"

**Constraints**

* ﻿﻿The returned JSON object contains either 0 or 1 record in data.
* ﻿﻿The country name may contain uppercase and lowercase English letters and ‹space> (ascii 32)

Note: Please review the header in the code stub to see available libraries for API requests in the selected language. Required libraries can be imported in order to solve the question. Check our full list of supported libraries at
[https://www.hackerrank.com/environment.](https://www.hackerrank.com/environment)

**• Input Format For Custom Testing**
In the first line, there is a country name.
In the second line, there is a phone number.

**• Sample Case 0**
  **Sample Input For Custom Testing**
    Afghanistan
    656445445

**Sample Output**

`+93 656445445`

**Explanation**
A call is made to API
[https://jsonmock.hackerrank.com/api/countries?name=Afghanistan.](https://jsonmock.hackerrank.com/api/countries?name=Afghanistan) The calling codes array contains 1 entry, '93'.

**• Sample Case 1**
  **Sample Input For Custom Testing**
    Puerto Rico
    564593986

**Sample Output**

`+1939 564593986`

**Explanation**
A call is made to the API to fetch the record for Puerto Rico. The returned callingCodes = ['1787, '1939']. Use the higher index code, callingCodes[1].

**• Sample Case 2**
  **Sample Input For Custom Testing**
    Oceania
    987574876

**Sample Output**

`-1`

**Explanation**
The API call return has an empty data array.

## Solution

#### Method 1:

```java
import java.io.*;
import java.math.*;
import java. security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util. function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;
import java.net.*;
import org.json.simple.*;
import org.json.simple.parser.*;
import java.net.http.*;
import java.net.URI;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;
import com. google.gson.*;

public class Result {
    public static String getPhoneNumbers(String country, String phoneNumber) {
        try {
            String encodedCountry = URLEncoder.encode(country, "UTF-8");
            String apiUrl = "https://jsonmock.hackerrank.com/api/countries?name=" + encodedCountry;
            URL url = new URL(apiUrl);
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            connection.setRequestMethod("GET");

            BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String inputLine;
            StringBuffer response = new StringBuffer();
            while ((inputLine = in.readLine()) != null) {
                response.append(inputLine);
            }
            in.close();

            JSONParser parser = new JSONParser();
            JSONObject jsonResponse = (JSONObject) parser.parse(response.toString());
            JSONArray data = (JSONArray) jsonResponse.get("data");

            if (data.isEmpty()) {
                return "-1";
            }

            JSONObject countryData = (JSONObject) data.get(0);
            JSONArray callingCodes = (JSONArray) countryData.get("callingCodes");

            if (callingCodes.isEmpty()) {
                return "-1";
            }

            String callingCode = (String) callingCodes.get(callingCodes.size() - 1);

            return "+" + callingCode + " " + phoneNumber;

        } catch (Exception e) {
            e.printStackTrace();
            return "-1";
        }
    }
}

public class Solution {
    public static void main(String[] args) {
         BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
         BUfferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
         String country = bufferedReader.readLine();
         String phoneNumber = bufferedReader.readLine();
         String result = Result.getPhoneNumbers(country, phoneNumber);
         bufferedWriter.write(result);
         bufferedWriter.newLine();

         bufferedReader.close();
         bufferedWriter.close();
    }
}
```


#### Method 2:

```java
import java.io.*;
import java.math.*;
import java. security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util. function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;
import java.net.*;
import org.json.simple.*;
import org.json.simple.parser.*;
import java.net.http.*;
import java.net.URI;
import org.json.simple.parser.JSONParser;
import org.json.simple.parser.ParseException;
import com. google.gson.*;

class Result {
    public static String getPhoneNumbers(String country, String phoneNumber) {
        try {
            String response = fetchCountryData(country);
            return parsePhoneNumber(response, phoneNumber, country);
        } catch (Exception e) {
            e.printStackTrace();
            return "-1";
        }
    }

    private static String fetchCountryData(String country) throws Exception {
        String encodedCountry = URLEncoder.encode(country, "UTF-8");
        String apiUrl = "https://jsonmock.hackerrank.com/api/countries?name=" + encodedCountry;
        URL url = new URL(apiUrl);
        HttpURLConnection connection = (HttpURLConnection) url.openConnection();
        connection.setRequestMethod("GET");

        BufferedReader in = new BufferedReader(new InputStreamReader(connection.getInputStream()));
        StringBuilder response = new StringBuilder();
        String inputLine;
        while ((inputLine = in.readLine()) != null) {
            response.append(inputLine);
        }
        in.close();

        return response.toString();
    }

    private static String parsePhoneNumber(String response, String phoneNumber, String country) throws ParseException {
        JSONParser parser = new JSONParser();
        JSONObject jsonResponse = (JSONObject) parser.parse(response);
        JSONArray data = (JSONArray) jsonResponse.get("data");

        if (data.isEmpty()) {
            return "-1";
        }

        JSONObject countryData = (JSONObject) data.get(0);
        JSONArray callingCodes = (JSONArray) countryData.get("callingCodes");

        if (callingCodes.isEmpty()) {
            return "-1";
        }

        String callingCode = (String) callingCodes.get(callingCodes.size() - 1);

        return "+" + callingCode + " " + phoneNumber;
    }
}

public class Solution {
    public static void main(String[] args) {
         BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
         BUfferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
         String country = bufferedReader.readLine();
         String phoneNumber = bufferedReader.readLine();
         String result = Result.getPhoneNumbers(country, phoneNumber);
         bufferedWriter.write(result);
         bufferedWriter.newLine();

         bufferedReader.close();
         bufferedWriter.close();
    }
}
```