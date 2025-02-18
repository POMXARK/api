# Resumes for employers

* Search for a CV
    * [Request and acceptable parameters](#search-params)
    * [Response](#search-results)

See also:

* [View a CV](https://github.com/hhru/api/blob/master/docs_eng/resumes.md#item)
* [Saved CV search](https://api.hh.ru/openapi/en/redoc#tag/Saved-resume-searches/operation/get-saved-resume-searches)

<a name="search-params"></a>
## Request and acceptable parameters

`GET /resumes` will return the results of CV search.

Some parameters take multiple values: `key=value&key=value`.

* `text` – search phrase. Finds CVs that have all the words from the set phrase.
  Several values can be indicated. Each additional
  `text` refines the search. You can use
  [search query language](http://hh.ru/article.xml?articleId=1175) as a search
  phrase. There is [autocompletion](suggests.md#resume-search-keyword) special
  for the field. To tune the phrase settings, you can use the following parameters:
  `text.logic`, `text.field`, `text.period`. When using extra `text.*` fields,
  you must indicate the whole set (triad) of parameters. If parameters are
  indicated incorrectly or there is an incorrect parameter set,
  `400 Bad request` will be returned.

* `text.logic` – describes how the search works. Directory with possible values:
  `resume_search_logic` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).

* `text.field` – describes where words from the `text` search
  phrase should be found. In the `text.field` parameter you can
  indicate several values separated by commas, e.g.
  `?text.field=education,keywords`. Directory with possible values:
  `resume_search_fields` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).

* `text.period` – a period for searching in work experience. The parameter
  works only when `text.field` equals one of: `experience`, `experience_company`,
  `experience_position`, `experience_description` parameters, but is must always
  be indicated when indicating other `text.*` parameters. In this case it can
  be empty.

---

For example:

* `GET /resumes?text=programmer` – will return all CVs that have the given word
  'programmer' in any place.
* `GET /resumes?text=programmer&text=java` – finds all CVs that have the words
  'programmer' and 'java' in any place.
* `GET /resumes?text=programmer%20java&text.logic=any&text.field=everywhere&text.period=all_time` –
  will find a CV that has a word from the given phrase in the `text` parameter
  ('programmer' or 'java') in any place. If extra fields are used, all of them
  must be indicated.
* `GET /resumes?text=Headhunter&text.logic=all&text.field=experience&text.period=last_three_years` –
  will find all CVs that have the word 'Headhunter' in the last 3 years' work experience.
* `GET /resumes?text=project%20manager&text.logic=all&text.field=experience%2Cskills&text.period=last_year&text=responsible&text.logic=all&text.field=everywhere&text.period=all_time` –
  will find all CVs that have the words 'project' and 'manager', and also
  'responsible' in any place of the work experience and key skills fields.
  It should be noted that extra parameters
  `text.logic=all&text.field=experience%2Cskills&text.period=last_year`
  are indicated for `text=project%20manager`, and
  `text.logic=all&text.field=everywhere&text.period=all_time` for the
  `text=responsible` parameter.

* `age_from`, `age_to` – the applicant's age in years, in the "from... to" range. Note that the search results will include resumes with unspecified age by default. To see resumes with specified age only, use the special [label](#resume_search_label) "only_with_age"
* `area` – region. Possible values reference: [/areas](https://github.com/hhru/api/blob/master/docs_eng/areas.md).
  You can indicate several values. CVs of applicants from
  indicated regions or those who ready to move to such regions
  are selected by default. Enter field `relocation` to change this behavior.
* `relocation` – willingness to relocate. Directory with possible values:
  `resume_search_relocation` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries). You can
  indicate it only with `area` parameter.
* `period` – in days, searches CVs published in the given time period.
  If not indicated, the search is performed without any restrictions on
  the publication date.
* `date_from` – the date the search should start from. The value is indicated in the
  [ISO 8601](https://github.com/hhru/api/blob/master/docs_eng/general.md#date-format) format – `YYYY-MM-DD`
  or with up-to-the-second precision `YYYY-MM-DDThh:mm:ss±hhmm`. You can't indicate it with the `period` parameter.
* `date_to` – a date until which the search should be performed. The value is indicated in the
  [ISO 8601](https://github.com/hhru/api/blob/master/docs_eng/general.md#date-format) format –
  `YYYY-MM-DD` or with up-to-the-second precision `YYYY-MM-DDThh:mm:ss±hhmm`. You can indicate it only with the
  `date_from` parameter. You can't indicate it with the `period` parameter.
* `education_level` – a level of education. Directory with possible values:
  `education_level` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries). If not indicated,
  the search is performed without any restrictions on the education level.
* `employment` – employment type.
  Directory with possible values: `employment` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries). You can indicate several values.
* `experience` – work experience. Directory with possible values: `experience`
  in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
* `skill` – key skills. At least one key skill identifier is indicated. You
  can get values from the `id` field in the
  [key skills suggestion](https://github.com/hhru/api/blob/master/docs_eng/suggests.md#key-skills).
* `gender` – a gender. Directory with possible values: `gender` in
  [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
<a name="resume_search_label"></a>
* `label` – an extra filter. Directory with possible values:
  `resume_search_label` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries). You can indicate
  several values.
* `language` – knowledge of a language. You can indicate several values. It is
  set in the language.level format, where:
    * `language` is a value from the [/languages](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-languages) directory,
    * `level` is a value from the `language_level`
      [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory.
* `metro` – a metro line or station. Directory with possible values:
  [/metro](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations).
* `currency` – a currency code. Directory with possible values: `currency`
  (code key) in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
* `salary_from`, `salary_to` – desired salary range, from...to.
* `schedule` – work schedule. Directory with possible values:
  `schedule` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries). You can indicate
  several values.
* `order_by` – CV list sorting. Directory with possible values:
  `resume_search_order` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
* `per_page` – the number of results per page (cannot exceed 50).
* `page` – a page number.
* `citizenship` – a desired country of citizenship. You can find possible
  values in the directory of countries. Several values can be indicated.
* `work_ticket` – a country which the applicant is permitted to work in.
  You can find possible values in the directory of countries. Several
  values can be indicated.
* `educational_institution` – the applicant's educational institutions.
  Suggestions on university names are used as parameters:
  [/suggests/educational_institutions](https://github.com/hhru/api/blob/master/docs_eng/suggests.md). Several values can be indicated.
* `search_in_responses` — `true`: search only in resumes with applicants who responded to vacancies of the current user's company,
`false`: search in all resumes. If this parameter is not specified, the search will take place in all resumes by default.
* `search_by_vacancy_id` — vacancy identifier. The search will be limited to the responses of this vacancy.
* `folder` — the ID of the folder with favourite resumes. The search will be limited to the contents of the specified folder.
Multiple folder IDs can be passed, for example: `folder=111&folder=222&folder=333`
* `include_all_folders` — a parameter indicating whether it is necessary to search through all folders with favourite resumes.
If a manager has access to favourite folders, the search will be limited to favourite folders by default.
If you pass the `include_all_folders=false` parameter, the search will not be limited to any folder.
The `400 Bad Request` error will be returned if `folder` and `include_all_folders` parameters are passed in the same request.
* `job_search_status` — job search status. 
Directory with possible values: `job_search_status` in [/dictionaries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-available-user-statuses). 
You can indicate several values.

If parameters contain an error, `400 Bad request` will be returned in response
with the error description in the body. Unknown parameters and parameters with
an error in the name are ignored.

When indicating paging parameters (page, per_page), a restriction takes effect:
the number of results returned can't exceed 2000. For instance, a request
`per_page=10&page=199` (displaying CVs from 1991 to 2000) is possible, but a
request with `per_page=10&page=200` will return an error (displaying CVs from
2001 to 2010).


<a name="search-results"></a>
### Response

When the authorized user is an applicant or anonymous, a `403` error will return.

```json
{
    "found": 2099341,
    "per_page": 20,
    "page": 0,
    "pages": 250,
    "items": [
        {
            "id": "0123456789abcdef",
            "title": "Aspiring specialist",
            "url": "https://api.hh.ru/resumes/0123456789abcdef",
            "first_name": "Ivan",
            "last_name": "Ivanov",
            "middle_name": "Ivanovich",
            "can_view_full_info": true,
            "age": 19,
            "alternate_url": "http://hh.ru/resume/0123456789abcdef",
            "created_at": "2015-02-06T12:00:00+0300",
            "updated_at": "2015-04-20T16:24:15+0300",
            "area": {
                "id": "1",
                "name": "Moscow",
                "url": "https://api.hh.ru/areas/1"
            },
            "certificate": [
                {
                    "achieved_at": "2015-01-01",
                    "owner": null,
                    "title": "test",
                    "type": "custom",
                    "url": "http://example.com/"
                }
            ],
            "education": {
                "primary": [
                    {
                        "name": "Russian State Social University, Moscow",
                        "name_id": "39420",
                        "organization": "Faculty of Information Technology",
                        "organization_id": null,
                        "result": "Computer science",
                        "result_id": null,
                        "year": 2012
                    }
                ]
            },
            "total_experience": {
                "months": 118
            },
            "experience": [
                {
                    "position": "shepherd",
                    "start": "2010-01-01",
                    "end": null,
                    "company": "Horns and Hoofs",
                    "industries": [
                        {
                            "id": "51.643",
                            "name": "Land and building improvement and cleaning"
                        },
                        {
                            "id": "29.503",
                            "name": "Farming, plant cultivation, cattle breeding"
                        }
                    ],
                    "company_url": "http://example.com/",
                    "area": {
                        "id": "1",
                        "name": "Moscow",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "company_id": null,
                    "employer": null
                },
                {
                    "start": "2005-01-01",
                    "end": "2009-03-01",
                    "company": "HeadHunter",
                    "area": {
                        "id": "1",
                        "name": "Moscow",
                        "url": "https://api.hh.ru/areas/1"
                    },
                    "industries": [
                        {
                            "id": "7.513",
                            "name": "Internet company (search engines, payment systems, social networks, educational resources, website promotion, etc)"
                        }
                    ],
                    "company_url": "http://hh.ru",
                    "company_id": "1455",
                    "employer": {
                        "alternate_url": "http://hh.ru/employer/1455",
                        "id": "1455",
                        "logo_urls": {
                            "90": "http://hh.ru/employer/logo/1455"
                        },
                        "name": "HeadHunter",
                        "url": "https://api.hh.ru/employers/1455"
                    }
                }
            ],
            "gender": {
                "id": "male",
                "name": "Male"
            },
            "salary": {
                "amount": 1000000,
                "currency": "RUR"
            },
            "photo": {
                "medium": "http://hh.ru/...",
                "small": "http://hh.ru/...",
                "id": "1337"
            },
            "owner": {
                "comments": {
                    "url": "https://api.hh.ru/applicant_comments/123456",
                    "counters": {
                        "total": 7
                    }
                }
            }
        }
    ],
    "platform": {
      "id": "headhunter"
    }
}
```

Field output settings in CV search don't affect output in the API.

CV is not fully displayed. The experience object lacks the description (the
`description` field), and the position (the `position` field) is available only
in the latest experience. Only the main education is displayed.

Contact information (full name) will be displayed only with paid access.

To obtain full information, you should request [the full CV](https://github.com/hhru/api/blob/master/docs_eng/resumes.md#item).
The applicant will have the CV request displayed in the view history.

CV fields are similar to the
[fields that are displayed when editing the CV](https://github.com/hhru/api/blob/master/docs_eng/resumes.md#resume-keys).

The employer will have additional fields:

* `owner.comments.url` containing url. GET request on it will return
  [applicant comments list of CV owner](https://api.hh.ru/openapi/en/redoc#tag/Applicant-comments/operation/get-applicant-comments-list).
* `owner.comments.counters.total` containing total comments amount.
