# Election Exit Poll Report

As part of HackerPoll's election exit poll analytics, a team needs a list of candidates with votes they received.

The result should be in the following format: candidate, votes.

* ﻿﻿candidate is a candidate's full name, the first_name and last name separated by a single space.
* ﻿﻿votes is a total count of all vote_at of the candidate.
* ﻿﻿Votes that cannot be matched to a candidate should be ignored.
* ﻿﻿Results should be sorted descending by votes, then ascending by candidate.

**Schema**

There are 2 tables:

|            | candidates |                      |
| :--------: | :---------: | :------------------: |
|    name    |    type    |     description     |
|     id     |  SMALLINT  |     Candidate ID     |
| first_name | VARCHAR(64) | Candidate First name |
| last_name | VARCHAR(64) | Candidate Last name |

|              |   results   |                |
| :----------: | :---------: | :------------: |
|     name     |    type    |  description  |
| candidate_id |  SMALLINT  |  Candidate ID  |
|   vote_at   | VARCHAR(19) | Vote timestamp |

**• Sample Data Tables**

For the sample data in tables:

|    | candidates |          |
| :-: | :--------: | :-------: |
| id | first_name | last_name |
| 1 |   Xavier   |   Ping   |
| 2 |  Westley  |  Drewell  |
| 3 |  Dominick  |  Scoble  |

|   results   |                    |
| :----------: | :-----------------: |
| candidate_id |       vote_at       |
|      0      | 2021-12-01 14:15:52 |
|      1      | 2021-12-01 03:55:23 |
|      1      | 2021-12-01 21:53:26 |
|      1      | 2021-12-02 07:57:40 |
|      1      | 2021-12-02 13:56:06 |
|      2      | 2021-12-01 11:46:40 |
|      2      | 2021-12-01 14:56:05 |
|      2      | 2021-12-01 21:54:50 |
|      2      | 2021-12-02 00:43:18 |
|      2      | 2021-12-02 06:59:33 |
|      2      | 2021-12-02 08:36:35 |
|      2      | 2021-12-02 10:20:33 |
|      2      | 2021-12-02 14:02:38 |
|      3      | 2021-12-01 05:18:34 |
|      3      | 2021-12-02 03:55:37 |
|      3      | 2021-12-02 05:30:24 |
|      3      | 2021-12-02 08:32:06 |
|      4      | 2021-12-02 05:05:55 |
|      5      | 2021-12-02 15:50:50 |
|      5      | 2021-12-02 20:45:00 |

the expected output is:

|    candidate    | votes |
| :-------------: | :---: |
| Westley Drewell |   8   |
|   Xavier Ping   |   4   |
| Dominick Scoble |   4   |

## Query Solution:

```mysql
SELECT 
    CONCAT(c.first_name, ' ', c.last_name) AS candidate, 
    COUNT(r.candidate_id) AS votes
FROM 
    candidates c
JOIN 
    results r 
ON 
    c.id = r.candidate_id
GROUP BY 
    c.id
ORDER BY 
    votes DESC, candidate ASC;
```
