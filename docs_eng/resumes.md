# CV

* [List of CVs for current user](#mine)
* [View a CV](#item)
  * [Additional fields for the resume publisher](#additional-author-fields)
  * [Resume-related paid services for the resume publisher](#applicant-paid-services)
  * [Additional fields for the employer](#additional-employer-fields)
  * [Resume-related paid services for the resume publisher](#paid-services)
* [Creating and editing a resume](#create_edit)
* [Publishing a resume](#publish)
* [Information on a resume's status and readiness for publication](#status-and-publication)
* [Cloning a resume](#clone)
* [Deleting a resume](#delete)
* [Checking for the ability to create a resume](#availability)
* [Conditions to fill in the fields of a resume](#conditions)
  * [Conditions to fill in the fields of a new resume](#init-conditions)
  * [Conditions for contacts in a resume](#conditions-contacts)
  * [Additional rules for resume fields](#conditions-other)
* [Resume abstract](#resume-nano)
* [Resume summary](#resume-short)
* [Resume download links](#download-links)
* [CV status](#status)
* [CV access type](#access_type)
  * [Resume visibility lists](#visibility_lists)
  * [Retrieving a list of resume visibility types](#get_access_types)
* [Resume viewing history](#views)
* [Searching for jobs similar to a resume](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)
* [CV hidden fields](#hidden-fields)


<a name="mine"></a>
## List of CVs for current user

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-mine-resumes)

<a name="item"></a>
## View a CV

> <img src="http://hhru.github.io/api/badges/emp_paid.png" alt="employer with paid access" /> : Methods require [paid access for the employer](/docs_eng/payable/employer_payable_methods.md)

```
GET /resumes/{resume_id}
``` 

>!! Note that there have been changes in access to contact details. Please read the information on [contact-by-contact resume access](payable/resume.md#contact-data) carefully

returns an indicated CV. If the CV visibility is set
to "visible to entire Internet" or "by direct link" (`everyone` and `direct`
respectively), it is possible to request the CV without being authorized.

An authorized publisher receives more detailed information, including the type of
visibility, comments of moderators, and status.

As for the employer, if it is not possible to view the full information on the resume given the current
authorization, some fields will contain `null`, and the `can_view_full_info` field will be `false`.

Once this URL has been requested, if the employer has an response/invitation for this resume, 
the response will be registered as viewed.

```json
{
    "id": "12345678901234567890123456789012abcdef",
    "last_name": "Last Name",
    "first_name": "First Name",
    "middle_name": "Middle Name",
    "age": 36,
    "birth_date": "1980-05-08",
    "gender": {
        "id": "male",
        "name": "Male"
    },
    "area": {
        "url": "https://api.hh.ru/areas/1",
        "id": "1",
        "name": "Moscow"
    },
    "metro": {
        "lat": 55.658147,
        "lng": 37.540957,
        "order": 19,
        "id": "6.41",
        "name": "Kaluzhskaya"
    },
    "relocation": {
        "type": {
            "id": "relocation_possible",
            "name": "ready to relocate"
        },
        "area": [
            {
                "url": "https://api.hh.ru/areas/2",
                "id": "2",
                "name": "St Petersburg"
            },
            {
                "url": "https://api.hh.ru/areas/76",
                "id": "76",
                "name": "Rostov-on-Don"
            }
        ]
    },
    "business_trip_readiness": {
        "id": "ready",
        "name": "Ready for business trips"
    },
    "contact": [
        {
            "verified": true,
            "comment": null,
            "type": {
                "id": "cell",
                "name": "Cellphone number"
            },
            "preferred": true,
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890"
            }
        },
        {
            "type": {
                "id": "email",
                "name": "Email"
            },
            "preferred": false,
            "value": "applicant@example.com"
        }
    ],
    "site": [
        {
            "url": "echo123",
            "type": {
                "id": "skype",
                "name": "Skype"
            }
        },
        {
            "url": "123456",
            "type": {
                "id": "icq",
                "name": "ICQ"
            }
        }
    ],
    "title": "Python programmer",
    "photo": {
        "small": "https://hh.ru/...",
        "medium": "https://hh.ru/...",
        "id": "1337"
    },
    "portfolio": [
        {
            "small": "https://hh.ru/...",
            "medium": "https://hh.ru/...",
            "id": "1337",
            "description": "..."
        }
    ],
    "salary": {
        "amount": 100500,
        "currency": "RUR"
    },
    "employments": [
        {
            "id": "full",
            "name": "Full time"
        },
        {
            "id": "part",
            "name": "Part time"
        }
    ],
    "schedules": [
        {
            "id": "fullDay",
            "name": "Full time"
        },
        {
            "id": "flexible",
            "name": "Flexible schedule"
        }
    ],
    "education": {
        "elementary": [
            {
                "name": "School №1923",
                "year": 2003
            }
        ],
        "additional": [
            {
                "name": "Refresher course",
                "organization": "Responsible organization",
                "result": "Specialization",
                "year": 2006
            }
        ],
        "attestation": [
            {
                "name": "IQ test",
                "organization": "IQ center",
                "result": "Intellect qualification",
                "year": 2005
            }
        ],
        "primary": [
            {
                "name": "K.I. Skryabin Moscow State Academy of Veterinary Medicine, Moscow",
                "name_id": "39464",
                "organization": "Faculty of Zootechnology and agrobusiness",
                "organization_id": "25181",
                "result": "Social Psychology",
                "result_id": null,
                "year": 2000
            }
        ],
        "level": {
            "id": "higher",
            "name": "Higher"
        }
    },
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "l1",
                "name": "native"
            }
        },
        {
            "id": "eng",
            "name": "English",
            "level": {
                "id": "b2",
                "name": "B2 - upper intermediate"
            }
        }
    ],
    "experience": [
        {
            "company": "Employer name",
            "company_id": null,
            "area": {
                "url": "https://api.hh.ru/areas/113",
                "id": "113",
                "name": "Russia"
            },
            "company_url": "http://www.rbc.ru",
            "industries": [
                {
                    "id": "7.540",
                    "name": "Software development"
                },
                {
                    "id": "9.399",
                    "name": "Mobile communication"
                }
            ],
            "position": "Position",
            "start": "2005-04-01",
            "end": "2013-01-01",
            "description": "Description of activity in the company"
        }
    ],
    "total_experience": {
        "months": 94
    },
    "skills": "Additional information: key skills",
    "skill_set": [
        "HTML",
        "CSS"
    ],
    "citizenship": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Russia"
        }
    ],
    "work_ticket": [
        {
            "url": "https://api.hh.ru/areas/113",
            "id": "113",
            "name": "Russia"
        }
    ],
    "travel_time": {
        "id": "any",
        "name": "Doesn't matter"
    },
    "recommendation": [
        {
            "name": "Petrov Pyotr",
            "position": "senior research scientist",
            "organization": "Roskosmos"
        }
    ],
    "resume_locale": {
        "id": "RU",
        "name": "Russian"
    },
    "certificate": [
        {
            "title": "Oracle Certified Java Professional Programmer",
            "achieved_at": "2013-01-01",
            "type": "custom",
            "owner": null,
            "url": "https://example.com/certificate/123456"
        },
        {
            "title": "MCSE: Windows NT 4.0",
            "achieved_at": "1998-01-26",
            "owner": "JOHN DOE",
            "type": "microsoft",
            "url": null
        },
    ],
    "alternate_url": "https://hh.ru/resume/12345678901234567890123456789012abcdef",
    "created_at": "2013-05-31T14:27:04+0400",
    "updated_at": "2013-10-17T15:22:55+0400",
    "download": {
        "pdf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/12345678901234567890123456789012abcdef/LastNameFirstNameMiddleName.rtf?type=rtf"
        }
    },
    "has_vehicle": true,
    "driver_license_types": [
        {
            "id": "A"
        },
        {
            "id": "B"
        }
    ],
     "hidden_fields": [
         {
             "id": "phones",
             "name": "All phone numbers listed in the CV"
         }
     ],
    "marked": false,
    "professional_roles": [
        {
            "id": 5,
            "name": "Technician"
        }
    ],
    "platform": {
      "id": "headhunter"
    }
}
```
<a name="resume-fields"></a>

Name | Type | Description
-----|-----|---------
id | string | Resume ID.
last_name | string or null | Last name.
first_name | string or null | First name.
middle_name | string or null | Middle name.
age | number or null | Age.
birth_date | string or null | Birthday (`YYYY-MM-DD`).
gender | [object](#id-name-object) or null | [Gender](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
area | [object](#id-name-url-object) or null | City of residence. [areas](areas.md) directory entry.
metro | [object](#metro-object) or null | The nearest metro station. [metro](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations) directory entry.
relocation | [object](#relocation-object) | Information on the possibility of moving to another city.
business_trip_readiness | [object](#id-name-object) | Readiness to go on business trips. [business_trip_readiness](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
contact | [array](#contact-object) | Applicant's contact list. 
photo | [object](#photo-object) or null | User photo.
portfolio | [array](#portfolio-object) | A list of images in the user's portfolio.
site | [array](#site-object) | Profiles in social networks and other services.
title | string or null | Desired position.
salary | [object](#salary-object) or null | Desired salary.
employments | [array](#id-name-object) | List of types of employment that are suitable for the applicant. [employment](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entries.
schedules | [array](#id-name-object) | List of working hours that are suitable for the applicant. [schedule](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entries.
education | [object](#education-object) | Education.
language | [array](#language-object) | List of languages spoken by the applicant. [languages](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-languages) directory entries. 
experience | [array](#experience-object) | Work experience.
total_experience | [object](#total-experience-object) or null | Total years of service.
skills | string or null | Additional information, a free-form description of skills.
skill_set | array | Key skills (a list of unique strings).
citizenship | [array](#id-name-url-object) | Applicant's citizenship list. Entries of the [directory of regions](areas.md).
work_ticket | [array](#id-name-url-object) | A list of regions where the applicant has a work permit. Entries of the [directory of regions](areas.md).
travel_time | [object](#id-name-object) | Acceptable travel time to the place of work. [travel_time](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
recommendation | [array](#recommendation-object) | List of recommendations.
resume_locale | [object](#id-name-object) | Resume language (locale). [Resume locales](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales-for-resume) directory entry.
certificate | [array](#certificate-object) | Applicant's certificate list.
alternate_url | string | URL for the resume on the website.
created_at | string | Date and time resume was created.
*download* | [object](#download-object) | Obsolete (use `actions`).
actions | [object](#actions-object) | Additional actions
updated_at | string | Date and time resume was updated.
has_vehicle | boolean or null | Does the applicant have their own car.
driver_license_types | [array](#driver-license-types-object) | A list of applicant's driving license categories.
hidden_fields | [array](#id-name-object) | List of hidden fields. Entry of the [resume_hidden_fields](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory ([more info](#hidden-fields)).
can_view_full_info | boolean or null | Possibility of getting resume contact info.
marked | boolean | Availability "Bright summary"
professional_roles | [array](#professional-role-object) | Array of professional role objects
platform | [object](#platform) | The platform on which the resume was posted


<a name="id-name-object"></a>
Object with id and name

Name | Type | Description
-----|-----|---------
id | string | Field Id.
name | string | Name of field.

<a name="id-name-url-object"></a>
Object with id, name and url

Name | Type | Description
-----|-----|---------
id | string | Field Id.
name | string | Name of field.
url | string | URL for getting information about the field.

<a name="metro-object"></a>
Object `metro`

Name | Type | Description
-----|-----|---------
id | string | Station ID.
name | string | Station name.
lat | number | Station latitude (a floating point number).
lng | number | Station longitude (a floating point number).
order | number | Sequence number of the station on the subway line (starting with 0).

<a name="relocation-object"></a>
Object `relocation`

Name | Type | Description
-----|-----|---------
type | [object](#id-name-object) | Willingness to relocate. [relocation_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
areas | [array](#id-name-url-object) | List of cities for potential relocation. Contains entries of the [directory of regions](areas.md).

<a name="contact-object"></a>
Object `contact`

Name | Type | Description
-----|-----|---------
type | [object](#id-name-object) | Contact type. [preferred_contact_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
value | string or [object](#value-object) | Contact value. Phone number: an [object](#value-object); email: a string.
preferred | boolean | Is this the preferred method of communication (should mention only one preferred contact as `"preferred": true`, if preferred flag is not sent default value for this parameter is `false`).
comment | string or null | Comment to the contact.
verified | boolean or null | Is the phone number confirmed (when specifying a phone number).

<a name="value-object"></a>
Object `value`

Name | Type | Description
-----|-----|---------
country | string | Country code (when specifying a phone number).
city | string | City code (when specifying a phone number).
number | string | Number (when specifying a phone number).
formatted | string | Formatted number (when specifying a phone number).

<a name="photo-object"></a>
Object `photo`

Name | Type | Description
-----|-----|---------
id | string | Unique image ID.
small | string | Small image URL. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
medium | string | URL for a medium-sized image. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.

<a name="portfolio-object"></a>
Object `portfolio`

Name | Type | Description
-----|-----|---------
id | string | Unique image ID.
small | string | Small image URL. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
medium | string | URL for a medium-sized image. This URL provides access to the image for a limited time after receiving a response. The application should be ready to receive `404 Not Found` as a response to the image request.
description | string or null | A description of the image in the portfolio.

<a name="site-object"></a>
Object `site`

Name | Type | Description
-----|-----|---------
type | [object](#id-name-object) | Profile type. [resume_contacts_site_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
url | string or null | A link to profile or ID.

<a name="salary-object"></a>
Object `salary`

Name | Type | Description
-----|-----|---------
amount | number | Amount
currency | string | [currency](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) ID.

<a name="education-object"></a>
Object `education`

Name | Type | Description
-----|-----|---------
elementary | [array](#elementary-object) | Secondary education. This field is usually only completed in the absence of higher education. 
additional | [array](#additional-education-object) | List of training courses.
attestation | [array](#additional-education-object) | List of passed tests or exams.
primary | [array](#primary-object) | List of degrees higher than secondary education.
level | [object](#id-name-object) | Education level. [education_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.

Features when saving `education`:
If you submit both higher education and secondary education and the education level is "secondary", only secondary education will be saved.
If you submit both higher education and secondary education and the education level is "higher", only higher education will be saved.

<a name="elementary-object"></a>
Object `elementary`

Name | Type | Description
-----|-----|---------
year | number | Year graduated.
name | string | Name of educational institution.

<a name="additional-education-object"></a>
Object with additional education

Name | Type | Description
-----|-----|---------
organization | string | The organization that conducted the courses/test/exam.
name | string | Course/test/exam name.
result | string or null | Profession/specialist area.
year | number | Year graduated/test/exam was passed.

<a name="primary-object"></a>
Object `primary`

Name | Type | Description
-----|-----|---------
name | string | Name of educational institution.
name_id | string or null | Educational institution ID.
organization | string | Faculty.
organization_id | string or null | Faculty ID.
result | string or null | Profession/specialist area.
result_id | string or null | Profession/specialist area ID.
year | number | Year graduated.

<a name="language-object"></a>
Object `language`

Name | Type | Description
-----|-----|---------
id | string | Language ID.
name | string | Language name.
level | [object](#id-name-object) | Language proficiency. [language_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.

<a name="experience-object"></a>
Object `experience`

Name | Type | Description
-----|-----|---------
company | string  or null | Organization.
company_id | string or null | Unique identifier of the organization. 
area | [object](#id-name-url-object) or null | Region of the organization. An entry in the [directory of regions](areas.md).
company_url | string or null | Company website.
industries | [array](#id-name-object) | A list of the company's industries. Entries of the [directory of industries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-industries).
position | string | Position.
start | string | Start date (`YYYY-MM-DD`).
end | string or null | End date (`YYYY-MM-DD`).
description | string | Responsibilities, functions, achievements.

<a name="total-experience-object"></a>
Object `total_experience`

Name | Type | Description
-----|-----|---------
months | number | An integer, the total months of service, rounded up to a month.

<a name="recommendation-object"></a>
Object `recommendation`

Name | Type | Description
-----|-----|---------
name | string | Name of person providing recommendation.
position | string | Position.
organization | string | Organization.

<a name="certificate-object"></a>
Object `certificate`

Name | Type | Description
-----|-----|---------
title | string | Certificate name.
achieved_at | string | Issue date (`YYYY-MM-DD`).
type | string | Certificate type. Available values: `custom`, `microsoft`.
owner | string or null | To whom the certificate is issued – only for certificates with `type = microsoft`.
url | string or null | A link to the page with the certificate description.

<a name="download-object"></a>
Object `download`

Name | Type | Description
-----|-----|---------
pdf | object | PDF resume.
pdf.url | string | A link to download a PDF resume.
rtf | object | RTF resume.
rtf.url | string | A link to download an RTF resume.

<a name="driver-license-types-object"></a>
Object `driver_license_types`

Name | Type | Description
-----|-----|---------
id | string | Applicant's driver’s license category. [driver_license_types](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.

<a name="professional-role-object"></a>
Object with id and name

Name | Type | Description
-----|-----|---------
id | string | Field Id.
name | string | Name of field.

<a name="platform"></a>
The platform on which the resume was posted

Name | Type | Description
-----|-----|---------
id | string | Platform. Available values: headhunter, zarplata, rabota

### Errors

* `403 Forbidden` - Incorrect authorization. Waiting for user authorization.
* `404 Not Found` – If the resume does not exist or is not available to the user.
* `429 Too Many Requests` - If the daily limit of resume views is exceeded (when the user is authorized as an employer).

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#resumes).


<a name="additional-author-fields"></a>
### Additional fields for the resume publisher

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "visible to all companies registered on HeadHunter"
        }
    },
    "blocked": false,
    "finished": false,
    "total_views": 0,
    "new_views": 0,
    "views_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/views",
    "status": {
        "id": "not_published",
        "name": "not published"
    },
    "can_publish_or_update": false,
    "next_publish_at": "2013-05-31T14:27:04+0400",
    "publish_url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/publish", 
    "progress": {
        "percentage": 42,
        "mandatory": [
            {
                "id": "citizenship",
                "name": "Citizenship"
            },
            {
                "id": "language",
                "name": "Languages"
            },
            {
                "id": "area",
                "name": "Area"
            },
            {
                "id": "skills",
                "name": "Skills"
            },
            {
                "id": "contact",
                "name": "Contacts"
            },
            {
                "id": "education",
                "name": "Education"
            }
        ],
        "recommended": [
            {
                "id": "salary",
                "name": "Salary"
            },
            {
                "id": "middle_name",
                "name": "Middle name"
            },
            {
                "id": "work_ticket",
                "name": "Work ticket"
            },
            {
                "id": "site",
                "name": "Site"
            },
            {
                "id": "recommendation",
                "name": "Recommendation"
            },
            {
                "id": "birth_date",
                "name": "Birth date"
            }
        ]
    },
    "moderation_note": [
        {
            "id": "bad",
            "name": "Резюме составлено небрежно."
        },
        {
            "id": "block_no_education_place_or_date",
            "name": "Отсутствуют данные об учебном заведении и дате его окончания.",
            "field": "education"
        }
    ],
    "paid_services": [
        {
            "id": "resume_autoupdating",
            "name": "Автообновление резюме",
            "active": false
        },
        {
            "id": "resume_marked",
            "name": "Яркое резюме",
            "active": true,
            "expires": "2016-06-08T18:25:25+0300"
        }
    ]
}
```

The fields `access`, `blocked`, `finished`, `total_views`, `new_views`, `status`, `views_url`
 are similar to those in the [current user resume list](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-mine-resumes).


#### Information on the publication/renew CV

 Name | Type | Description
 ---- | ----| --------
 can_publish_or_update | boolean | Is it possible to [publish or update this resume](#publish)
 next_publish_at | string | Date and time for next CV renew possibility
 publish_url | string | An URL to publish or update the resume

<a name="author-progress"></a>
#### Information on the resume completion percentage

The resume publisher can see the information on the resume completion percentage in the `progress` field:

 Name | Type | Description
 ---- | ----| --------
 percentage | number | Resume completion percentage
 mandatory | array | A list of required fields that have not been filled in yet
 mandatory[].id | string | Field ID
 mandatory[].name | string | Field name
 recommended | array | A list of recommended fields that have not been filled in yet
 recommended[].id | string | Field ID
 recommended[].name | string | Field name


<a name="author-moderation-notes"></a>
#### Moderator's comments

The moderator can add comments to the resume to the following list:
`moderation_note`. In some cases, comments can lead to
[resume banning](#status). A full list of comments is available
[in the `resume_moderation_note` directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).


The following fields are available for comments:

Name | Type | Description
--- | --- | ---
id | string | comment ID
name | string | comment description
field | string or отсутствует | resume field associated with the comment

<a name="applicant-paid-services"></a>
#### Resume-related paid services for the resume publisher

Resume-related paid services for the resume publisher are displayed in the `paid_services` field.

The following fields are available for each service:

Name | Type | Description
--- | --- | ---
id | string | service ID
name | string | service name
active | logical | information on whether the service is currently enabled
expires | string (date) | service expiration time, if the service is enabled


<a name="additional-employer-fields"></a>
### Additional fields for the employer

```json
{
    "can_view_full_info": false,
    "owner": {
        "id": "123456",
        "comments": {
            "url": "https://api.hh.ru/applicant_comments/123456",
            "counters": {
                "total": 7
            }
        }
    },
    "paid_services": [
        {
            "id": "resume_database_access",
            "name": "Access to the resume database",
            "price_list": {
                "alternate_url": "https://hh.ru/price#dbaccess"
            },
            "quick_purchase": {
                "alternate_url": "https://hh.ru/employer/invoice/purchase?code=FA&hhAreaId=1&period=1&profAreaIds=0",
                "currency": {
                    "abbr": "руб.",
                    "code": "RUR",
                    "name": "Rubles"
                },
                "name": "Buy for 5000 rubles",
                "price": 5000
            },
            "description": "To view a candidate's hidden contacts and photos, purchase access to the resume database."
        }
    ],
    "negotiations_history": {
        "url": "https://api.hh.ru/resumes/12345678901234567890123456789012abcdef/negotiations_history",
        "vacancies": [
            {
                "id": "321",
                "name": "Test vacancy",
                "url": "https://api.hh.ru/vacancies/321",
                "archived": false,
                "items": [
                    {
                        "employer_state": {
                            "id": "offer",
                            "name": "Offer"
                        },
                        "created_at": "2017-01-30T15:06:47+0300",
                        "with_message": true
                    }
                ],
                "negotiations_url": "https://api.hh.ru/negotiations/123",
                "messages_url": "https://api.hh.ru/negotiations/123/messages"
            }
        ]
    }
}
```

<a name="actions-object"></a>
Object `actions` (additional actions)

Name | Type | Description
-----|--|---------
download | [object](#download-object) | Links to download a resume in multiple formats ([learn more](#download-links)).
download_with_contact | [object](#download-object) or null | Links to download resume with contacts (the service is spent) in multiple formats ([learn more](#download-links)).
get_with_contact | object or null | Link to get resume with contacts (the service is spent).
get_with_contact.url | string | Link to get resumes with contacts. Returns an object similar to [viewing a resume](#item)
viewed | logic | field of resume object obtained from the [search request](resumes_search.md). It has value `true` if employer viewed CV
When contacts are viewed via `download_with_contact` and `get_with_contact` it may transpire that the user has hidden their contact details([learn more](docs_eng/payable/resume.md#viewing-of-resumes-with-contact-info)), yet the viewing will be debited regardless while the reply body will return null in the respective contact data fields. To safeguard against this, make sure the fields you want are available in [hidden_fields](#hidden-fields) the resume.
The URL in the fields `download_with_contact` and `get_with_contact` is generated automatically and will be different every time.

<a name="paid-services"></a>
### Resume-related paid services for the employer

An employer may be offered a list of paid resume-related services.

For example, if the full resume information is not available, the employer will receive
an offer to purchase a recommended service that allows such access.

The list of services is displayed in the `paid_services` list. The following fields are available for each service:

Name | Type | Description
--- | --- | ---
id | string | service ID
name | string | service name
price_list.alternate_url | string | link to the site where the full price for the service is available
quick_purchase | object, null | a quick service purchase, if available
quick_purchase.alternate_url | string | link to the site where you will be asked to buy a service
quick_purchase.name | string | name of the action for the service order
quick_purchase.price | nubmer | price of service
quick_purchase.currency | object | currency of service
description | string, null | service use note


<a name="owner-field"></a>
#### Information on the resume owner

The `owner` field contains the following information on the resume owner:

Name | Type | Description
--- | --- | ---
id | string | Resume owner ID
comments | object | [comments for the resume owner](https://api.hh.ru/openapi/en/redoc#tag/Applicant-comments/operation/get-applicant-comments-list)
comments.url | string | The URL to perform a GET request to obtain the list of comments
comments.counters | object | information on the number of comments
comments.counters.total | number | total number of comments

<a name="negotiations-history-field"></a>
#### Brief history of responses/invitations for a resume

The `negotiations_history.url` field is always available and contains the URL to perform a GET request to obtain the
[detailed history of responses/invitations for a resume](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-resume-negotiations-history).

The `negotiations_history.vacancies` is available only when
the following additional parameter was passed when executing the [request for resume](resumes.md#item):
`with_negotiations_history`. In this case, the GET request should look like this:

`GET /resumes/{resume_id}?with_negotiations_history=true`

The format of the `negotiations_history.vacancies` field is described on the
[detailed history of responses/invitations for a resume](https://api.hh.ru/openapi/en/redoc#tag/Employer-responsesinvitations/operation/get-resume-negotiations-history) page, and the only difference is that
in this case, the list will be limited to 3 jobs of this employer and the latest status change
for the response/invitation for each of these jobs.

<a name="viewed-field"></a>
#### Flag, indicating whether the resume has been viewed by employer

The `viewed` field is always given and may take on the values `true` or `false`.

<a name="create_edit"></a>
## Creating and editing a resume

`POST /resumes` — adding a resume

`PUT /resumes/{resume_id}` — editing an existing resume. JSON of the same format as sent for a GET request
                             is used as a request body. In this case, only id of transferred data is used
                             for the fields with the directory data from the transferred JSON structure. 
                             For example, in a resume, in the languages field, Russian is indicated as the native language:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "native",
                "name": "native"
            }
        }
     ]
   }
```

To add English with "B2 - upper intermediate" level send the following JSON:

```json
{
    "language": [
        {
            "id": "rus",
            "name": "Russian",
            "level": {
                "id": "l1",
                "name": "native"
            }
        },
        {
            "id": "eng",
            "level": {
                "id": "b2"
            }
        }
    ]
  }
```

The first element is Russian, which we already have in languages, the second is
the new element, English, that we want to add. Fields `language.name` and
`language.level.name` in this case are not in the way but also do not carry useful information.

Sending data replaces existing data for the selected parameter.
Each parameter can be sent separately.

<a name="resume-keys"></a>
> Also, read the rules for filling the fields in the [Conditions to fill in the fields of a resume](#conditions)

<a name="resume-edit-params"></a>
Parameters:

* `last_name` — second name;
* `first_name` — first name;
* `middle_name` — middle name;
* `birth_date` — date of birth (YYYY-MM-DD);
* `gender` — gender. Directory entries [gender](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
* `photo` — user photo. see. [artifacts](https://api.hh.ru/openapi/en/redoc#tag/Artifact-managing);
* `portfolio` — user portfolio. see [artifacts](https://api.hh.ru/openapi/en/redoc#tag/Artifact-managing);
* `area` — place of residence. Directory entries [areas](areas.md);
* `metro` — nearest metro station. Directory entries [metro](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-metro-stations). If you submit a metro station that does not exist in submitted area, the field will be ignored;
  It makes sense to show only for `area` with metro;
* `relocation` — possible relocation. Consists of the fields:
    * `type` — Directory entries [relocation_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
    * `area` — relocation city (list). Makes sense only with the corresponding `type` field. Directory entries
      [areas](areas.md);
* `business_trip_readiness` — agree to go on business trips. Directory entries
  [business_trip_readiness](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
* `contact` — contact info (list). 
Mandatory of the contact fields see in [conditions to fill in the fields of a resume](#conditions)
Consists of the fields:
    * `type` — Directory entries [preferred_contact_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
    * `value` — contact value. For phone number, consists of four fields (`country`, `city`, `number`, `formatted`); 
    for email: a string.
    * `preferred` — preferred type of communication (`true` or `false`);
    * `comment` — comment to the contact;
* `site` — presence on other websites. Consists of the fields:
    * `type` — type of website. Directory entries [resume_contacts_site_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
    * `url` — a link to a profile or an ID on a third-party website/service;
* `title` — desired position;
* `professional_roles` — candidate's professional roles (list). Directory entries
      [professional_roles](https://api.hh.ru/openapi/redoc#tag/Obshie-spravochniki/operation/get-professional-roles-dictionary)
* `salary` — Desired salary. It consists of the following fields:
    * `amount` — total;
    * `currency` — [currency](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) ID;
* `employments` — Employment. [employment](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entries.
* `schedules` — work schedule. List of directory [schedule](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) entries
* `education` — education. Consists of the fields:
    * `elementary` — secondary education (list). This field is usually only completed in the absence of higher education.
     It consists of the following fields:
        * `year` — year graduated;
        * `name` — name of educational institution;
    * `additional` — further training courses (list). It consists of the following fields:
        * `organization` — the organisation that conducted the course;
        * `name` — name of the course;
        * `result` — profession / specialist area;
        * `year` — year graduated;
    * `attestation` — tests, exams (list):
        * `organization` — the organisation that conducted the test or exam;
        * `name` — name of the test or exam;
        * `result` — profession / specialist area;
        * `year` — year the test/exam was passed;
    * `primary` — education higher than secondary (list). It consists of the following fields:
        * `name` — name of educational institution;
        * `name_id` — the id of the educational institution can be found in the [tips for college names](suggests.md#universities);
        * `organization` — faculty;
        * `organization_id` — faculty ID can be found in the [faculties directory](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-faculties);
        * `result` — profession / specialist area;
        * `result_id` — specialisation id can be found in the [tips for specialisations](suggests.md#specializations);
                        education level;
        * `year` — year graduated;
    * `level` — education level. Directory entries [education_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)
* `language` — languages (list):
    * `id` - value from [languages](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-languages)
    * `level` - value from [language_level](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries).
* `experience` — work experience (list). It consists of the following fields:
    * `company` — company;
    * `company_id` — company id, can be found in the [tips for companies](suggests.md#companies);
    * `area` — region of the company. Directory entries [areas](areas.md);
    * `company_url` — company website;
    * `industries` — A list of the company's industries. Entries of the [directory of industries](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-industries)
    * `position` — position;
    * `start` — started work (YYYY-MM-DD);
    * `end` — finished work (YYYY-MM-DD);
    * `description` — responsibilities, functions, achievements;
* `skills` — additional information, a free-form description of skills;
* `skill_set` — key skills (a list of unique strings).
* `citizenship` — citizenship (list). Directory entries [areas](areas.md);
* `work_ticket` — work permit (list). Directory entries [areas](areas.md);
* `travel_time` — acceptable travel time to the place of work. Directory entries [travel_time](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries);
* `recommendation` — recommendations (list). It consists of the following fields:
    * `name` — name;
    * `position` — position;
    * `organization` — company;
* `resume_locale` — resume locale. Directory entries [локали резюме](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-locales-for-resume).
* `driver_license_types` - A list of applicant's driving license categories. [driver_license_types](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.
* `has_vehicle` - Does the applicant have their own car;
* `hidden_fields` - [hidden fields](#hidden-fields) in the resume (list). Directory entry
* `access` - [resume visibility](#access_type)
    * `type` - visibility type. Directory entry [resume_access_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries)

Parameters taken from [tips](suggests.md) (`name_id`, `organization_id`, `result_id`, `company_id`) 
are optional. In this case, if these parameters are indicated, then when saved they are checked for
being correct. In case of errors, such as non-existent
ids or unconnected university and faculty ids, it will return `HTTP 400 Bad Request` with an indication
of the parent field containing the error.
Additionally, when writing `company_id` in the work experience, the company name will
be changed to the company name from the tips.

### Response

A successful response to resume creation comes with a code `201 Created`, and
the Location header will contain the URL of the created resume:

```
Location: /resumes/0123456789abcdef
```

A successful response to resume update comes with a code and does not have a body.


### Errors

* `403 Forbidden` – The request is not from the applicant.
* `400 Bad Request` - Errors in resume fields. You will receive additional [extended information](#resume-validation) on errors.
* `404 Not Found` – The resume was not found or is not available to the current user (during an update)
* `400 Bad Request` - The allowable number of resumes is exceeded (during creation)
In addition, an [error will be specified](errors.md#resumes) with `type=resumes`, `value=total_limit_exceeded`.


<a name="resume-validation"></a>
### Errors in using fields when creating and editing resumes

When creating and editing resumes, the values in the fields are validated to check the format of used fields and values (see [Parameters](#resume-edit-params)), existence of data, and business rules.

In the event of errors, the response will be `400 Bad Request` with the following body:
```json
{
   "errors": [
        {
            "type": "bad_json_data",
            "value": "year",
            "reason": "min_value",
            "description": "Value is too low",
            "pointer": "/education/additional/1/year"
        },
        {
            "type": "bad_json_data",
            "value": "access",
            "reason": "required",
            "description": "ID for access to resume is a required field",
            "pointer": "/access/type/id"
        }
    ]
}
```
Name | Type | Description
--- | --- | ---
type | string | Error class (always takes the value of `bad_json_data`)
reason | string | Error reason
value | string | Field where the error was found
description | string | Error description for user
pointer | string | [Data pointer](#error-pointer) with error in incoming message

Validation error extends [standard API error](errors.md#general-errors).

Possible causes of errors:

Code | Explanation
--- | ---
required | this field is required
not_found | no value found for submitted id
faculty_without_university | you cannot set the faculty without the university
not_in_dictionary | no value was found in the directory for submitted id
not_a_leaf | value cannot include any leaf node
end_date_before_start_date | `end` less than `start`
not_country | 'area' must be a country (see [country directory](areas.md#countries))
more_than_one_native_language | more than one native language
must_contain_unique | submitted values must be unique
from_different_profareas | submitted values are from different industries
duplicate | value was already used
bad_image_type | submitted value is of bad type (`portfolio` requires values from `GET /artifacts/portfolio`, `photo` requires values from `GET /artifacts/photo`)
processing | object is being processed
preferred_must_be_unique | preferred method of communication must be unique
preferred_contact_not_specified | preferred method of communication is not specified or contact is not specified
need_country_city_number_or_formatted | wrong telephone format in contact details (see [conditions for completing the contact details in the resume](#conditions-contacts))
invalid | error in field value (fields must comply with [conditions for completing the fields](resumes.md#conditions))
greater_than_max | value is greater than the maximum value
less_than_min | value is less than the minimum value
earlier_than_min | date is earlier than allowed
later_than_max | date is later than allowed
length_less_than_min | character number in the field is less than the minimum
length_greater_than_max | character number in the field is greater than the maximum
size_less_than_min | number of items is less than the minimum
size_greater_than_max | number of items is greater than the maximum
send_metro_without_area | no `area` specified for submitted metro station
not_belong_this_city | this metro station is not in the specified city
required_with_not_started_career | submit work experience if the specialty was not the career start
not_match_regexp | value does not match regular expression
more_than_one | more than one email sent
not_available | provided not available value

<a name="error-pointer"></a>
`pointer` for identifying the value uses JsonPointer format [RFC 6901](https://tools.ietf.org/html/rfc6901).
For example, `/education/additional/1/year` means that that the error in the field comes from the message (`year` must be a number):
```json
{
    "title": "Python programmer",
    "education": {
        "additional": [
            {
                "name": "Initial training course",
                "organization": "Training organization",
                "result": "General knowledge of Python",
                "year": 2006
            },
            {
                "name": "Further training course",
                "organization": "Training organization",
                "result": "In-depth knowledge of Python",
                "year": "2012 - error"
            }
        ]
   },
   "salary": {
        "amount": 100500,
        "currency": "RUR"
   }
}
```


<a name="publish"></a>
## Publishing a resume

`POST /resumes/{resume_id}/publish`

The resume can be used as soon as it is first published.

Subsequent publications will update the renewal date of the resume. `next_publish_at` key
in the resume indicates when the resume can be updated.


### Response

A successful response contains a code `204 No Content` and is body-less.


### Errors

* `429 Too Many Requests` - If the update is not available yet.
* `400 Bad Request` - If publication/extension is not possible. The possible causes are:
  * Mandatory fields are empty (to understand what exactly is not filled in, you can call the url [get resume](#item) and look at the `mandatory` field),
  * The fields have not been not edited after banning by a moderator,
  * The resume is being checked by a moderator.
* `403 Forbidden` - If the resume cannot be published because of a lack of necessary privileges (for example, for an employer).


<a name="status-and-publication"></a>
## Information on a resume's status and readiness for publication

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-information/operation/get-resume-status)

<a name="clone"></a>
## Cloning a resume

`POST /resumes?source_resume_id={resume_id}`

Successful cloning will return the response code `201 Created` and the header
`Location` of the response will contain the link to the new resume.

You can only clone your own resumes, otherwise the response code
will be `404 Not Found`.

<a name="delete"></a>
## Deleting a resume

```
DELETE /resumes/{resume_id}
```

where `resume_id` – resume ID.

This method is only available to applicants. The resume is deleted without the possibility of
restoration. All responses associated with this resume are also deleted.

### Response

A successful response contains a code `204 No Content` and is body-less.

### Errors

* `403 Forbidden` – The request is not from the applicant.
* `404 Not Found` – The resume was not found or is not available to the current user.

<a name="availability"></a>
## Checking for the ability to create a resume

### Request

```
GET /resumes/creation_availability
```

### Response

Successful server response is returned with `200 OK` code and contains:

```json
{
    "is_creation_available": true,
    "max": 20,
    "created": 2,
    "remaining": 18
}
```

where:

Name | Type | Description
---- | ------ | ---
is_creation_available  | boolean | This is a flag that indicates whether the creation of new resumes is available to this user
max | number | Maximum number of resumes
created  | number | The number of previously created resumes
remaining  | number | The number of resumes that can be created

### Errors

* `403 Forbidden` – The request is not from the applicant.

<a name="conditions"></a>
## Conditions to fill in the fields of a resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-resume-conditions)

<a name="init-conditions"></a>
## Conditions to fill in the fields of a new resume

> >!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Field-conditions/operation/get-new-resume-conditions)

<a name="conditions-contacts"></a>
## Conditions for contacts in a resume
When filling out contacts in a resume, take the following into account:

 * The resume must contain an email address (and only one).

 * The resume must contain a phone number, and there can be only one number for each type.
   
 * Comments are only available for phone numbers, a comment for an email will not be saved.

 * In the `email` contact, the value is email, for phone it is the object.


Example message for changing contacts in the resume:

```json
{
    "contact": [
        {
            "type": {
                "id": "email"
            },
            "value": "box@test.ru"
        },
        {
            "type": {
                "id": "cell"
            },
            "value": {
                "country": "7",
                "city": "123",
                "number": "4567890",
                "preferred": true
            }
        },
        {
            "type": {
                "id": "home"
            },
            "value": {
                "formatted": "7(499)9078456"
            },
            "comment": "On phone before 9 PM"
        }
    ]
}
```

You must provide either the whole phone number in the `formatted` field or all three parts of the phone number separately in 
the fields `country`, `city` and `number`. If both options are available, the system uses data from the separate fields.
The `formatted` field may contain additional symbols: spaces, brackets, and hyphens.
The separate fields may only contain numbers.


<a name="conditions-other"></a>
## Additional rules for resume fields

There are other rules for filling out a resume outside of the
above-described format:

 * It is not allowed to create several resumes with the same title.

 * Specialisation must be from the same area of profession.

 * The place of residence must be obtained from the `/areas` directory and the selected city cannot
      contain daughter objects, for example, the user cannot indicate
      "Russia" as the place of residence.

 * The nearest metro station must be located in the place of residence.

 * For specialisations from the area *Start of career, students* (id=15) it is not necessary to specify work experience. 
 For other areas of profession these fields must contain at least one entry.

 * Some of the fields of the resume are read-only and cannot be changed with POST/PUT at /resumes.
   

<a name="resume-nano"></a>
## Resume abstract

The briefest resume abstract:

```json
{
    "id": "502ff8b100018bddf30039ed1f63735f4dda66",
    "title": "manager",
    "url": "https://api.hh.ru/resumes/502ff8b100018bddf30039ed1f63735f4dda66"
}
```

where:

 Name  | Type    | Description
 ---- | ------ | ---
 id   | string | Resume ID
 title | string | Desired position
 url  | string | Link to the full resume


<a name="resume-short"></a>
## Resume summary

This option differs from the detailed display in the absence of some fields.

```json
{
    "id": "0123456789abcdef",
    "title": "Resume",
    "url": "https://api.hh.ru/resumes/0123456789abcdef",
    "first_name": "Ivan",
    "last_name": "Ivanov",
    "middle_name": "Ivanovich",
    "can_view_full_info": true,
    "age": 19,
    "alternate_url": "https://hh.ru/resume/0123456789abcdef",
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
                "name": "National Research Nuclear University, Moscow",
                "name_id": "39420",
                "organization": "Faculty of Information Technologies",
                "organization_id": null,
                "result": "Computer science",
                "result_id": null,
                "year": 2012
            }
        ],
        "level": {
            "id": "higher",
            "name": "Higher"
        }
    },
    "total_experience": {
        "months": 118
    },
    "experience": [
        {
            "position": "shepherd",
            "start": "2010-01-01",
            "end": null,
            "company": "Horns and hooves",
            "industries": [
                {
                    "id": "51.671",
                    "name": "Landscaping, Cleaning of Buildings and Outdoor Areas"
                },
                {
                    "id": "29.531",
                    "name": "Agriculture, Crop Production, Livestock Breeding"
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
                "name": "Москва",
                "url": "https://api.hh.ru/areas/1"
            },
            "industries": [
                {
                    "id": "7.541",
                    "name": "Internet Company (Search Engines, Payment Systems, Social Networks, Information and Educational, Entertainment Resources, Website Promotion etc.)"
                }
            ],
            "company_url": "https://hh.ru",
            "company_id": "1455",
            "employer": {
                "alternate_url": "https://hh.ru/employer/1455",
                "id": "1455",
                "logo_urls": {
                    "90": "https://hh.ru/employer/logo/1455"
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
        "medium": "https://hh.ru/...",
        "small": "https://hh.ru/...",
        "id": "1337"
    },
    "owner": {
        "id": "123456",
        "comments": {
            "url": "https://api.hh.ru/applicant_comments/123456",
            "counters": {
                "total": 7
            }
        }
    },
    "negotiations_history": {
        "url": "https://api.hh.ru/resumes/0123456789abcdef/negotiations_history"
    },
    "download": {
        "pdf": {
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/FirstLastMiddle.pdf?type=pdf"
        },
        "rtf": {
            "url": "https://hh.ru/api_resume_converter/0123456789abcdef/FirstLastMiddle.rtf?type=rtf"
        }
    }
}
```

<a name="download-links"></a>
## Resume download links

At the moment, resumes can be downloaded in the following formats: PDF and RTF.
Applicants can download their resumes. 
The name of the downloaded file may contain the applicant's name or desired position.

### Request

To download a resume, you need to use the URL obtained from the API response, while passing [standard API headers](general.md#request-requirements).

```
GET https://....(a link obtained in the full or shortened resume from the API)
```

### Response

A successful response comes with a code and contains the requested file in its body.

### Errors

* `404 Not Found` - If the resume does not exist or is not available to the user.
* `429 Too Many Requests` - If the daily limit of resume views is exceeded (when the user is authorized as an employer).
* `403 Forbidden` - Services not sufficient to download resume with contacts

In addition to the HTTP code, the server can return a description of the [error cause](errors.md#resumes).


<a name="status"></a>
## CV status

The `status` key determines the current status of the resume and contains an entry from the
[resume_status](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory. After creating a new resume, it
gets the `not_published` status. No one can see a resume with this status,
the user begins to fill in and save the resume (empty mandatory fields
are present in the `progress.mandatory` list). 

After all mandatory fields are filled in, the `can_publish_or_update` flag 
will become `true`, and the resume will be available for
[publication](#publish). After publication, the resume gets the `published` status.
A resume with this status is searchable if permitted by the settings for
[resume visibility](#access_type).

After receiving the `published` status, the resume is available for moderators and
can be banned (the `blocked` status), if the fields are invalid or
contain insufficient information. Reasons for banning a resume can be found in
the [`moderation_note` key](#author-moderation-notes). A banned resume
is not searchable and cannot be used to respond to a job.

After editing, the resume can be sent to the moderator for secondary revision.
In this case, the resume status changes to `on_moderation` and from there it can
go to `blocked` again or to `published`, depending on the moderator's decision.

Once the resume is published (status changed to `published`) it cannot be changed back to
`not_published` but it can be hidden in the [resume visibility](#access_type) settings.

In `published` status, the resume can be used to [apply for jobs](negotiations.md) and it will appear on the
[list of suitable vacancies](suitable_resumes.md) if it has not been used yet to apply for this job.


<a name="access_type"></a>
## CV access type

Each resume has the `access` visibility setting that determines to whom the resume will be available
in the search results or using a direct link. The field's format in the resume:

```json
{
    "access": {
        "type": {
            "id": "clients",
            "name": "visible to all companies registered on HeadHunter"
        }
    }
}
```

After publication, the resume can be searched by all employers. Otherwise,
for example, when a job is found and you want to hide the resume in the search results, you should change
the resume visibility settings. The "access.type" key is responsible for this. Visibility type is a
[resume_access_type](https://api.hh.ru/openapi/en/redoc#tag/Public-directories/operation/get-dictionaries) directory entry.

<a name="access_type_restrictions"></a>
‼️ Since September 1, 2021, the type of resume visibility with the id `everyone` (visible to entire internet) has become unavailable for saving due to legal restrictions.

 Code | Description
 --- | --------
 no_one | A resume of this type is not visible to anyone. However, it can be used to apply for a vacancy and the resume type will change to `whitelist`.
 whitelist | The resume is visible only to the specified companies. If you respond to a job of a company that is not listed, that company will be automatically included in the list. Please see [resume visibility lists](#visibility_lists).
 blacklist | РThe resume can be searched and viewed by all companies, except for ones specified. If you respond to a job of a company that is blacklisted, that company will be automatically excluded from the black list. Please see [resume visibility lists](#visibility_lists).
 clients | The resume is visible to all companies registered on hh.ru.
 everyone | The resume is visible to all users (everywhere on the Internet). This type [is not available for saving](#access_type_restrictions).
 direct |The resume is visible only with a direct link (link specified in the `alternate_url` key).


<a name="visibility_lists"></a>
### Resume visibility lists


Some types of visibility, such as `whitelist` and `blacklist`, imply the use of a list of employers
who can or cannot see the resume. Please see [managing resume visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists).


<a name="get_access_types"></a>
### Retrieving a list of resume visibility types

#### Request

```
GET /resumes/{resume_id}/access_types
```

where:
* `resume_id` — resume ID

Successful server response is returned with `200 OK` code and contains:

```json
{
    "items": [
        {
            "id": "everyone",
            "name": "visible to entire internet"
        },
        {
            "id": "no_one",
            "name": "invisible"
        },
        {
            "id": "clients",
            "name": "is visible to all companies registered on Headhunter"
        },
        {
            "id": "whitelist",
            "name": "visible to selected companies",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/whitelist",
            "total": 3,
            "limit": 2000
        },
        {
            "id": "blacklist",
            "name": "hidden from selected companies",
            "list_url": "https://api.hh.ru/resumes/{resume_id}/blacklist",
            "total": 5,
            "limit": 2000,
            "active": true
        },
        {
            "id": "direct",
            "name": "available only by direct link"
        }
    ],
    "auto_hide_time_options": [
        {
            "id": "month_12",
            "name": "1 year"
        },
        {
          "id": "month_10",
          "name": "10 months",
          "active": true
        },
        {
            "id": "month_8",
            "name": "8 months"
        }
    ]
}
```

#### Response

Name | Type | Description
----|-----|---------
items | array | Available resume visibility types.
items[].id | string | Visibility type ID.
items[].name | string | Visibility type name.
items[].active | boolean or null | Visibility type selection indicator.
items[].list_url | string | List address (only for "blacklist" and "whitelist" types).
items[].total | number | Number of companies in the corresponding visibility list (only for `blacklist` and `whitelist` types).
items[].limit | number | Maximum number of companies in the visibility list (only for `blacklist` and `whitelist` types).
auto_hide_time_options | array | Resume auto hide by user inactivity time options, this field is only available for rabota.by users.
auto_hide_time_options[].id | string | Auto hide option ID.
auto_hide_time_options[].name | string | Auto hide option name.
auto_hide_time_options[].active | boolean or null | Auto hide option selection indicator.

#### Errors

* `403 Forbidden` — The user is not an applicant.
* `404 Not Found` — A resume with this ID was not found or is not available to the current user.


Please see also [managing resume visibility lists](https://api.hh.ru/openapi/en/redoc#tag/Resume-visibility-lists).


<a name="views"></a>
## Resume viewing history

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Resume.-Viewing-info/operation/get-resume-view-history)

<a name="similar"></a>
## Searching for jobs similar to a resume

The information is available only to the resume publisher.

### Request

>!! Method is defined in [OpenAPI](https://api.hh.ru/openapi/en/redoc#tag/Applicant-vacancy-search/operation/get-vacancies-similar-to-resume)

<a name="hidden-fields"></a>
## CV hidden fields

The `hidden_fields` field contains a list of search fields hidden by the applicant. Hidden fields are replaced by `null`. The CV author is provided with relevant data.

* `names_and_photo` enters `null` instead of the values of the `first_name`, `last_name`, `middle_name` and `photo` fields
* `phones`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `cell,` `work,` or `home`
* `email`  enters `null` instead of the value of the `contact[].value` field, when `contact[].type` contains `email`
* `other_contacts` enters `null` instead of the value of the `site[].url` field
* `experience` enters `null` instead of the values of the `experience[].company`, `experience[].company_id`, `experience[].company_url`, `experience[].employer` fileds; enters an empty list instead of the value of the `recommendation` field

