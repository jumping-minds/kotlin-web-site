# Kotlin website
[![Official project][project-badge]][project-url]

This repository is the source for [https://kotlinlang.org](https://kotlinlang.org).

* [Website structure](#website-structure)
* [Contribution](#contribution)
* [Local deployment](#local-deployment)
* [Feedback and issues](#feedback-and-issues)

<a id="project-structure"></a>
## Website structure 

### Content

|Website page|Source files|
|------------|--------|
| [Main page](https://kotlinlang.org/) | [templates/pages/index.html](templates/pages/index.html) |
| [Kotlin docs](https://kotlinlang.org/docs/home.html) |[docs/topics](docs/topics)| 
| [Community](https://kotlinlang.org/community/) | [pages/community](pages/community) | 
| [Education](https://kotlinlang.org/education/) | [templates/pages/education](templates/pages/education)| 

Note that source files for the [server-side landing page](https://kotlinlang.org/lp/server-side/) and [Kotlin Multiplatform Mobile landing page](https://kotlinlang.org/lp/mobile/) are not publicly available.

#### Sources in different repositories

Source files for coroutine docs, and language specification are stored in separate repositories:

|Website page|GitHub repository|
|------------|--------|
| [Coroutine docs](https://kotlinlang.org/docs/coroutines-guide.html) | [kotlinx.coroutines](https://github.com/Kotlin/kotlinx.coroutines/docs) |
| [Language specification](https://kotlinlang.org/spec/introduction.html) | [kotlin-spec](https://github.com/Kotlin/kotlin-spec) |

#### Auto-generated content

[API reference documentation](https://kotlinlang.org/api/latest/jvm/stdlib/) is generated based on comments in the Kotlin code. 
Learn more about [documenting the Kotlin code](https://kotlinlang.org/docs/kotlin-doc.html).

The [Kotlin grammar reference](https://kotlinlang.org/docs/reference/grammar.html) is generated by the [Kotlin grammar generator](https://github.com/JetBrains/kotlin-grammar-generator) from the
[Kotlin grammar definition](https://github.com/JetBrains/kotlin/tree/master/grammar).

### Configuration files

|Configuration| File                                                                                 |
|-----|--------------------------------------------------------------------------------------|
|Navigation and structure| [kr.tree](docs/kr.tree) for docs and [_nav.yml](data/_nav.yml) for other pages       |
|Variables, such as release version | [v.list](docs/v.list) for docs and [releases.yml](data/releases.yml) for other pages |
|Community events on the map | [events.xml](data/events.yml)                                                          |
|Video list (outdated) | [videos.yml](data/videos.yml)                                                        |

### Templates

The Kotlin website uses [Jinja2](https://jinja.palletsprojects.com/en/2.11.x/) templates from the [templates](templates) directory.
Note that all Markdown files, except for [docs](docs), are processed as Jinja templates before HTML conversion. 
This allows using all Jinja benefits for Markdown (for example, building URLs with the `url_for` function).

## Contribution

You can contribute to the Kotlin website by sending us a pull request. If you're going to propose a big change, discuss your idea with the team via [doc-feedback@kotlinlang.org](mailto:doc-feedback@kotlinlang.org).

For the Kotlin documentation, follow [these guidelines on style and formatting](https://docs.google.com/document/d/1mUuxK4xwzs3jtDGoJ5_zwYLaSEl13g_SuhODdFuh2Dc/edit?usp=sharing).

For other pages, follow the complete syntax reference at the [kramdown site](https://kramdown.gettalong.org/syntax.html).
You can also include metadata fields. Learn more in the [Jekyll docs](https://jekyllrb.com/docs/front-matter/).

### Kotlin User Group
To add a Kotlin User Group, proceed the following way:
1) open the configuration file [user-groups.yml](/data/user-groups.yml);
2) find a suitable section among existing ones;
3) add into the selected section a new group with followed keys:
    - `name`, the name of the group.
    - `country`, the name of the country where the group is located. In the case of a virtual group, please use "International" for that. 
    - `url`, the link to the group's web page.
    - `isVirtual`, set this key with `true` value if the group is online only.
    - `position`, the geo-position of the group, defined by pair of keys: `lat` and `lng`. It better to run `scripts/user_group`
4) If the group is not virtual, you also need to specify a group's position.
   You can do it manually adding `position` key with the `lat` and `lng` values, as next: 
   ```yaml
   position:
     lat: 1.1111111
     lng: 1.1111111
   ```
   or, to run the geo script (`scripts/user_groups_geolocator.py`) that will do it for you.
   You need to obtain GOOGLE_API_KEY and then run the following script:
   ```
   $ GOOGLE_API_KEY="..." python scripts/universities_geolocator.py
   ```
   More details about GOOGLE_API_KEY param you can find in [this article](https://developers.google.com/maps/documentation/geocoding/get-api-key).
   The manual way sometimes is better, because it allows you to specify the position more precisely.  

You can see the structure and types of the expected configuration in [the JSON schema](/data/schemas/user-groups.json).
Once you publish a Pull Request, the changes will be validated by [GitHub Actions Workflow](.github/workflows/validate-user-groups-data.yml) to prevent misconfiguration.

### Community Events
To add an event to the Community Events, follow the instruction below. 
1) Fill the event info in the [events.yml](/data/events.yml) with the next:
   - `lang`, two-letter code considering [ISO 639-1 format](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes).
   - `startDate`, in the format 'yyyy-mm-dd'.
   - `endDate`, in the format 'yyyy-mm-dd'. For the on day event fill the same date as in the startDate.
   - `location`, in form of 'City, Country'.
   - `speaker`, the speaker's name.
   - `title`, event's title.
   - `subject` a title of a talk.
   - `url` link to the event web page.
   You can see the structure and types of the expected configuration in [the JSON schema](/data/schemas/events.json).
2) Publish the changes creating a Pull Request. The changes will be validated by [GitHub Actions Workflow](.github/workflows/validate-events-data.yml) to prevent misconfiguration.

## Local deployment

Currently, there is no way to deploy the Kotlin website locally. This ticket tracks the effort of adding support for local testing: [KT-47049](https://youtrack.jetbrains.com/issue/KT-47049).

You can contribute to the Kotlin website by sending us a pull request.

## Feedback and issues

You can:

* Share feedback in the [#docs-revamped](https://kotlinlang.slack.com/archives/C01GGPPCAA0/p1607340719000500) channel in our Kotlin public Slack ([get an invite](https://surveys.jetbrains.com/s3/kotlin-slack-sign-up)).
* Report an issue to [our issue tracker](https://youtrack.jetbrains.com/newIssue?project=KT&c=tag%20kotlin-doc-migration).
* Email us at [doc-feedback@kotlinlang.org](mailto:doc-feedback@kotlinlang.org).

[project-url]: https://confluence.jetbrains.com/display/ALL/JetBrains+on+GitHub
[project-badge]: https://jb.gg/badges/official.svg
[slack-url]: https://slack.kotlinlang.org

## Pages on Next.js

You can find all pages in the "pages" directory.

### Projects Structure

- **Components**. The building blocks.
- **Blocks**. Blocks are groups of components joined together to form a relatively complex, distinct section of an interface.
- **Pages**. Each page is associated with a route based on its file name.

### Images in Next.js
Notice that using 'next/image' is not possible because Next.js does not support importing images to HTML files (SSG).
Use Img and Svg components from "next-optimized-images" instead.
