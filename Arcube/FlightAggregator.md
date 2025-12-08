# **Problem Statement**

You work for a flight/tour aggregator that receives multiple offers for the **same itinerary** from different providers such as airlines, Online Travel Agencies (OTAs), and consolidators.

### Examples of Providers:

* **Airlines:** IndiGo (6E), Air India (AI), SpiceJet (SG), Emirates (EK), Lufthansa (LH), British Airways (BA)
* **OTAs:** MakeMyTrip (MMT), Cleartrip (CLT), Expedia (EXP), Booking.com (BKG)
* **Consolidators:** Via.com (VIA), TripJack (TJK), Yatra (YTR)

For each itinerary, you must select **one “best” offer** based on the business rules defined below.

---

## **Input Format**

The program must read from standard input (`System.in`) in the following format:

### **Line 1: Search Criteria**

```
CURRENCY MAX_STOPS MAX_TOTAL_DURATION REQUIRE_BAG
```

| Field              | Type    | Description                             | Example |
| ------------------ | ------- | --------------------------------------- | ------- |
| CURRENCY           | String  | The currency code for filtering offers  | EUR     |
| MAX_STOPS          | Integer | Maximum number of stops allowed         | 2       |
| MAX_TOTAL_DURATION | Integer | Maximum total flight duration (in minutes) | 600     |
| REQUIRE_BAG        | Boolean | Whether baggage inclusion is mandatory  | true    |

---

### **Line 2: Number of Offers**

```
N
```

* **N** is the total number of offers (0 ≤ N ≤ 10000)

---

### **Next N Lines: Offer Details**

Each line represents one offer in the following format:

```
OFFER_ID ITINERARY_ID PROVIDER_CODE PRICE CURRENCY STOPS TOTAL_DURATION INCLUDES_BAG REFUNDABLE
```

| Field              | Type    | Description                             | Example |
| ------------------ | ------- | --------------------------------------- | ------- |
| OFFER_ID           | String  | Unique identifier for the offer (no spaces)  | OFF801     |
| ITINERARY_ID       | String  | Identifier for the itinerary (no spaces)  | ITN100     |
| PROVIDER_CODE      | String  | Code representing the provider (no spaces) | 6E     |
| PRICE              | Decimal | Price of the offer (up to 2 decimal places) | 150.00     |
| CURRENCY           | String  | Currency code of the offer | EUR     |
| STOPS              | Integer | Number of stops in the itinerary         | 1       |
| TOTAL_DURATION     | Integer | Total flight duration in minutes         | 320     |
| INCLUDES_BAG       | Boolean | Whether checked baggage is included      | true    |
| REFUNDABLE         | Boolean | Whether the ticket is refundable         | false    |

---


## **Output Format**

For every itinerary that has at least one valid offer, print one line:
```
ITINERARY_ID BEST_OFFER_ID
```
 - Output must be sorted in **ascending lexicographical order** by ITINERARY_ID
 - If **no itinerary** has any valid offers, the program should produce no output.

## **Business Rules**

## **1. Filtering (Invalid offers are discarded)**

An offer is considered **INVALID** and must be ignored if **any** of the following conditions is true:

| Condition                                     | Reason                           |
| --------------------------------------------- | -------------------------------- |
| OFFER_ID is missing or empty                  | Incomplete data                  |
| ITINERARY_ID is missing or empty              | Incomplete data                  |
| CURRENCY is null, empty, or ≠ search CURRENCY | Currency mismatch                |
| PRICE ≤ 0                                     | Invalid price                    |
| STOPS > MAX_STOPS                             | Exceeds maximum allowed stops    |
| TOTAL_DURATION > MAX_TOTAL_DURATION           | Exceeds maximum allowed duration |
| REQUIRE_BAG == true AND INCLUDES_BAG == false | Baggage requirement not met      |

Only offers that **pass all checks** are considered **valid**.

---

## **2. Grouping**

Group all valid offers by their **ITINERARY_ID**.

---

## **3. Selection (Choosing the Best Offer per Itinerary)**

For each itinerary, select **exactly one** best offer using the following priority (in order):

| Priority | Criterion         | Preference                      |
| -------- | ----------------- | ------------------------------- |
| 1        | Price             | Lowest price wins               |
| 2        | Baggage inclusion (if prices are equal) | INCLUDES_BAG = true wins        |
| 3        | Refundability (if still tied) | REFUNDABLE = true wins          |
| 4        | Total duration (if still tied) | Shorter duration wins           |
| 5        | Provider code (if still tied) | Lexicographically smallest wins |

**Note:**
If an itinerary has no valid offers after filtering, it should **not appear** in the output.

---

## **Constraints**

 - ```0 <= N <= 10000```
 - Prices are positive decimals with up to 2 decimal places
 - ```CURRENCY```, ```ITINERARY_ID```, ```OFFER_ID```, ```PROVIDER_CODE``` do not contain spaces.
 - The solution should handle upto 10000 offers efficiently.

---

## **Example**

### **Input**

```
EUR 2 600 true
5
OFF001 ITN100 6E 150.00 EUR 1 320 true false
OFF002 ITN100 MMT 150.00 EUR 1 300 true true
OFF003 ITN100 EK 200.00 EUR 0 280 true true
OFF004 ITN200 LH 180.00 EUR 1 400 false false
OFF005 ITN200 AI 190.00 EUR 1 350 true false
```

---
## **Explanation**

**Search Criteria:**
Currency = EUR, Max Stops = 2, Max Duration = 600 mins, Require Bag = true

| Offer  | Itinerary | Valid? | Reason                                |
| ------ | --------- | ------ | ------------------------------------- |
| OFF001 | ITN100    | ✓      | Passes all checks                     |
| OFF002 | ITN100    | ✓      | Passes all checks                     |
| OFF003 | ITN100    | ✓      | Passes all checks                     |
| OFF004 | ITN200    | ✗      | INCLUDES_BAG = false but bag required |
| OFF005 | ITN200    | ✓      | Passes all checks                     |

### **Selection for ITN100**

* OFF001 and OFF002 both have price = 150.00 (lowest)
* Both include baggage
* OFF002 is refundable, OFF001 is not → **OFF002 wins**

### **Selection for ITN200**

* Only OFF005 is valid → **OFF005 wins**

---

## **Output**

```
ITN100 OFF002
ITN200 OFF005
```

---

## **Your Task**

Write a Java program that:

1. Reads input from standard input (`System.in`) in the format described above.
2. Applies all filtering and selection rules.
3. Prints the final mapping of ```ITINERARY_ID BEST_OFFER_ID``` to standard output, one per line, **sorted by ITINERARY_ID**.

---

## **Requirements**

* The program must compile and run as a **single Java file** named `Solution.java`.
* It must contain a ```public static void main(String[] args)``` method.
* You may create helper classes, methods, or data structures within the same file.

---



## Solution

#### Method 1:

```java
/**
 * You are given:
 * - A list of Offer objects (offers)
 * - SearchCriteria (criteria)
 *
 * Implement selectBestOffers so that it:
 *
 * 1) Filters invalid offers:
 *   - itineraryId is null or empty → discard
 *   - currency is null/empty or not equal to criteria.currency → discard
 *   - price <= 0 → discard
 *   - stops > criteria.maxStops → discard
 *   - totalDurationMinutes > criteria.maxTotalDurationMinutes → discard
 *   - criteria.requireBagIncluded == true AND includesBag == false → discard
 *
 * 2) Groups remaining offers by itineraryId.
 *
 * 3) For each itinerary, selects ONE best offer using this priority:
 *      i)   Lowest price
 *      ii)  If tie → includesBag == true preferred
 *      iii) If tie → refundable == true preferred
 *      iv)  If tie → shorter totalDurationMinutes preferred
 *      v)   If tie → lexicographically smallest providerCode preferred
 *
 * 4) Returns a map: itineraryId → bestOfferId
 *    - Itineraries with no valid offers must NOT appear in the map.
 */

class Offer {
  final String offerId;
  final String itineraryId;
  final String providerCode;
  final BigDecimal price;
  final String currency;
  final int stops;
  final int totalDurationMinutes;
  final boolean includesBag;
  final boolean refundable;

  Offer(String offerId,
        String itineraryId,
        String providerCode,
        BigDecimal price,
        String currency,
        int stops,
        int totalDurationMinutes,
        boolean includesBag,
        boolean refundable) {

    this.offerId = offerId;
    this.itineraryId = itineraryId;
    this.providerCode = providerCode;
    this.price = price;
    this.currency = currency;
    this.stops = stops;
    this.totalDurationMinutes = totalDurationMinutes;
    this.includesBag = includesBag;
    this.refundable = refundable;
  }
}

class SearchCriteria {
  final String currency;
  final int maxStops;
  final int maxTotalDurationMinutes;
  final boolean requireBagIncluded;

  SearchCriteria(String currency,
                int maxStops,
                int maxTotalDurationMinutes,
                boolean requireBagIncluded) {

    this.currency = currency;
    this.maxStops = maxStops;
    this.maxTotalDurationMinutes = maxTotalDurationMinutes;
    this.requireBagIncluded = requireBagIncluded;
  }
}


class Solution {
  public Map<String, String> selectBestOffers(List<Offer> offers, SearchCriteria criteria) {
    // Write your code here

    List<Offer> valid = new ArrayList<>();

    // Filtering out invalid offers
    for (Offer o : offers) {

        if (o.offerId == null || o.offerId.isEmpty()) continue;
        if (o.itineraryId == null || o.itineraryId.isEmpty()) continue;
        if (o.currency == null || o.currency.isEmpty() || !o.currency.equals(criteria.currency)) continue;
        if (o.price.compareTo(BigDecimal.ZERO) <= 0) continue;
        if (o.stops > criteria.maxStops) continue;
        if (o.totalDurationMinutes > criteria.maxTotalDurationMinutes) continue;
        if (criteria.requireBagIncluded && !o.includesBag) continue;

        valid.add(o);
    }

    // grouping valid offers by itineraryId
    Map<String, List<Offer>> byItinerary = new HashMap<>();
    for (Offer o : valid) {
        byItinerary.computeIfAbsent(o.itineraryId, k -> new ArrayList<>()).add(o);
    }

    // Selecting best offer per itinerary
    Map<String, String> result = new TreeMap<>();
    for (String itin : byItinerary.keySet()) {
        List<Offer> list = byItinerary.get(itin);

        list.sort((a, b) -> {

            int comparedPrice = a.price.compareTo(b.price);
            if (comparedPrice != 0) return comparedPrice;

            if (a.includesBag != b.includesBag)
                return a.includesBag ? -1 : 1;

            if (a.refundable != b.refundable)
                return a.refundable ? -1 : 1;

            if (a.totalDurationMinutes != b.totalDurationMinutes)
                return Integer.compare(a.totalDurationMinutes, b.totalDurationMinutes);

            return a.providerCode.compareTo(b.providerCode);
        });

        result.put(itin, list.get(0).offerId);
    }

    return result;
  }
}
```
