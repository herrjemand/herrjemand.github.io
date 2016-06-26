---
title   : Countries
info    : World countries in JSON, CSV, XML and Yaml.
github  : mledoze/countries
web     : https://git.io/countries
pid     : 20160104facv
---

Countries project was created by Mohammed Le Doze, a developer from France. It contains a lists of world countries, their name, international codes, languages, capital, location, translations and other information.

My main contribution was development and implementation of new language, name and translation structure. Here is the original structure:

```json
{
        "name": "New Zealand",
        "nativeName": "New Zealand",
        ...
        "language": ["English", "M\u0101ori", "New Zealand Sign Language"],
        "languageCodes": ["en", "mi"],
        "translations": {
            "fr": "Nouvelle-Z\u00e9lande",
            "nl": "Nieuw-Zeeland",
            ...
        }
        ...
}
```

There two main problems in this structure:

 - Name and native name share common prefix. They should be a single object. Official name is missing. Some countries like UK have common name(UK), and official name(United Kingdom of Great Britain and Northern Ireland).
 - Languages and language codes are not corresponding to each other. There three languages, and two language codes. In best case scenario, when there is N languages and N language codes, you would have to map one array to another array, praying that all information in right order.

So I decided to create new, cleaner, well structured way of to store name and languages. During my research other issues occurred:

 - There is no *native* language. For seventy-four countries on the planet Earth, there is more than one official language. For example New Zealand. It's official languages are English, Maori and Sign language. Currently we having one, that is clearly not representing picture. So we needed to store all official languages.
 - Alpha-2 codes(two character language codes), could not be used, as there a lot of languages with no Alpha-2 codes, so Alpha-3 codes must be used.
 - Alpha-2 to Alpha-3 db needed to be created. Alpha-3 language names db needed to be created.
 - Countries languages had to be checked.
 - There is no databases of official names, so Wikipedia parcer, that would retrieve official name from html had to be written, and then I manually had to them all.
 - Translations had to be upgraded to correspond new language structure, and there is no easy way to get translated official names, so python translator script, that would use google translate api had to be written.
 - The volume of changes that needed to be done was massive, so automation editing tools were created.
 - Preservation of the original code style was crucial, to maintain low entrance for future editors.

The result was worth the hard work:

```json
    {
        "name": {
            "common": "New Zealand",
            "official": "New Zealand",
            "native": {
                "eng": {
                    "official": "New Zealand",
                    "common": "New Zealand"
                },
                "mri": {
                    "official": "Aotearoa",
                    "common": "Aotearoa"
                },
                "nzs": {
                    "official": "New Zealand",
                    "common": "New Zealand"
                }
            }
        },
        ...
        "languages": {
            "eng": "English",
            "mri": "Māori",
            "nzs": "New Zealand Sign Language"
        },
        "translations": {
            "deu": {"official": "Neuseeland", "common": "Neuseeland"},
            "fra": {"official": "Nouvelle-Zélande", "common": "Nouvelle-Zélande"},
            ...
        },
        ...
    }
```

New format made project better structured, easier to maintain, more useful and insanely more popular(we gained more than fifteen hundred stars in a week).

I have gained a lot of knowledge about languages and countries, frankly improving my geography skills. I have improved my web parsing skills that I have used in many projects since then. I also gained a friend, and became maintainer of the Countries project.

I am continuing bug fixing, solving issues, answering questions, opening pull requests and continuing develop this awesome project.

I am very grateful to my dear friend [Mohammed](https://github.com/mledoze/) for allowing me do all those contributions, and for creating such an amazing project.