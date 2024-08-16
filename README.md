# DotaDocumentation

## Introduction
Just a simple ReadMe for my website I made so I can remember how I designed the website and what practices I should follow

## Table of Contents

- [Frontend Documentation](#Frontend-Documentation)
- [Backend Documentation](#Backend-Documentation)
- [Database design](#Database-Design)

## Frontend Documentation
Next.js is used for SEO purposes. DaisyUI components are also used to help speed up development

- **Tech Stack**: React, Next.js, Tailwind CSS, DaisyUI

## Libraries Used
- **`nivo-charts`**: Used to create interactive and customizable charts to visualize Dota 2 statistics and performance metrics. Provides a variety of chart types with responsive and interactive features.
- **`dota2-hero-sprites`**: Utilized to integrate high-resolution hero sprites into the application


## Project Structure

### File and Folder Organization

- **/components**: Contains all reusable UI components.
  - **/Charts**: Contains charts components used for analysis.
  - **/herocounters**: Contains components used for herocounters section.
  - **/overview**: Contains components used for Profile overview page.
  - **/misc**: Contains misc card/row components.

- **/app**: Contains the main pages of the application.
  - **/builds**: Contains the builds page and builds specific components.
  - **/counters**: Contains the counters page and counters specific components.
  - **/items**: Contains the items page and items specific components.
  - **/neutrals**: Contains the neutrals page and neutrals specific components.
  - **/profile**: Contains the profile page and profile specific components.
  - **/synergy**: Contains the synergy page and synergy specific components.

- **/public**: Contains the images and svgs needed for the project.

- **/utils**: Contains necessary utility functions needed for certain calculation/hero name finder.

- **/dota2-herosprites**: Contains necessary files needed for using the dota hero image sprites.


## Optimization 

### Performance Optimization
- **Total Blocking Time (TBT)**: Reduce unnecessary javascript and calculations
- **Cumulative Layout Shift (CLS)**: Measures to prevent unexpected layout shifts. Ensure containers have fixed widths or predefined dimensions to avoid layout changes while data is being loaded
- **Code Splitting**: Use of code splitting for faster load times, especially in analysis portion where numerous data will be fetched from server side, certain data can be fetch asynchronously in the client side with code splitting.
- **Cache**: Use Nextjs' inbuilt cache mechanism
- **Image optimzation**: Item images are currently served from a CDN (from steam) while other images should be wrapped around Nextjs' Image component
- **Static Site Generation (SSG)**: Use SSG to pre-render pages at build time, the data on the page isn't dynamic

### Data Fetching Strategies
- **Server Component Wrapping**: Wrap all client components in a server component where HTTP requests are fired off to fetch data from the database. By consolidating data fetching into server components, you can leverage server-side rendering (SSR) to pre-fetch data before sending the page to the client. This reduces client-side load and speeds up the initial page load.


### Semantic HTML
- **Usage of Semantic Tags**: Use of `<header>`, `<footer>`, `<nav>`, `section` etc.

### Performance Testing
- **Tools**: Lighthouse for core web vitals testing



## Backend-Documentation

### Overview
The backend of the DotaRecaps application is built to handle user requests, process data, and manage interactions with the database. 
As of now it is currently built using Nextjs. In the future, it ought to be replaced by ExpressJS and also using Reddis for caching

### Tech Stack
- **Languages**: JavaScript (Node.js)
- **Frameworks**: Next.js
- **Databases**: Supabase
- **API design**: RESTful

<!-- ### Architecture
- **High-Level Architecture**: [Diagram showing API servers, database, and caching layers]
- **Components**: Includes an API server, authentication service, and data storage.
- **Data Flow**: Data is processed through API requests, validated, and then stored in PostgreSQL. -->
### Scripts File and Folder Organization
- **/scripts**: Contains scripts for complex data retrieval.
  - **test.js**: Script for executing all scripts required to daily data retrieval.
  - **/herocounters**: Contains scripts for fetching data related to matchups and synergies.
    - **`fetchHeroID.js`**: Retrieves data related to Heroes and their descriptions.
    - **`fetchTierList.js`**: Retrieves data related to hero stats.
    - **`fetchVSHerostats.js`**: Retrieves data related to hero matchups in general.
    - **`fetchVSLanestats.js`**: Retrieves data related to hero matchups in lane.
    - **`fetchWITHHerostats.js`**: Retrieves data related to hero synergies in general.
    - **`fetchWITHLanestats.js`**: Retrieves data related to hero synergies in lane.

  - **/items**:  Contains scripts for fetching data related to builds, items and neutral items statistics.
    - **`fetchItems.js`**: Retrieves data related to hero matchups, including counters and synergies.

  - **/lastpatch**: Scripts for fetching data related to items from last patch.
    - **`fetchItemsLP.js`**: Retrieves data related to hero matchups, including counters and synergies.

  - **/profile**: Scripts for fetching data for profile analysis uses.
    - **`fetchdata.js`**: Retrieves data related to profile analysis script 1.
    - **`fetchdata2.js`**: Retrieves data related to profile analysis script 2.
    - **`fetchEnemyStats.js`**: Retrieves data related to the user's enemies stats performance.
    - **`fetchHeroData.js`**: Retrieves data related to user's heroes stats performance script 1.
    - **`fetchMyAvgData.js`**: Retrieves data related to user's heroes stats performance script 2.
    - **`fetchWardData.js`**: Retrieves data related to the user's ward data.

## Data Processing and Optimization Practices

### Data Processing Techniques

- **Pre-Processing**: Initial data preparation to ensure data is clean and properly formatted before further processing.
- **Batch Processing**: Use batch processing to efficiently handle bulk data insertion, so as to reduce the amount of database transactions done, significantly reducing processing time.
- **Asynchronous Operations**: Use asynchronous operations to perform concurrent tasks, so as to insert/fetch data faster.

### Optimization Strategies

- **Caching**: Use Nextjs' in-built cache system.
- **Rate Limiting**: Configure rate limiting to manage API usage and prevent abuse, ensuring platform stability and reliability.

### API Design
  - All API endpoints are secured and require a valid access token to access. The access token must be included in the `Authorization` header of the request. This token is validated to ensure that only authorized users can access or modify data.



<!-- ### Security
- **Encryption**: SSL/TLS is used to encrypt data transmitted between the client and server.
- **Authorization**: Role-based access control (RBAC) for managing user permissions.
- **Vulnerability Management**: Regular security audits and updates to address vulnerabilities. -->

<!-- ### Deployment
- **Infrastructure**: Deployed on AWS using EC2 instances.
- **CI/CD**: Implemented CI/CD pipelines with GitHub Actions for automated testing and deployment.
- **Monitoring and Logging**: Utilized Prometheus for monitoring and ELK Stack for logging.

### Testing
- **Unit Testing**: Jest is used for unit testing individual components.
- **Integration Testing**: Postman for testing API endpoints.
- **End-to-End Testing**: Cypress for end-to-end testing of user interactions. -->


## Database Design
This section details the design of the database for Dotarecaps application. It includes the normalization process, Entity-Relationship Diagram (ERD), entity relationships, primary keys, foreign keys and indexes.

DotaRecaps was first designed using a de-normalized database back when i didn't know much about a good database design. Looking back at the database, I realised the poor design resulted in large amount of data redundancy, and a lack of usage of foreign keys to maintain data integrity and indexes to improve query speeds. Therefore, I decided to re-design a proper 3NF Database. However, this is only the design and the project hasn't yet migrated to this new design as it requires changing alot of queries that would take some time

### Normalization to 3NF
The database design process involved normalizing the schema to Third Normal Form (3NF) to minimize redundancy and ensure data integrity. 

**Normalization Steps:**
1. **First Normal Form (1NF):** Ensured that each table had a primary key and that all columns values were broken down to atomic values. The initial design had fields that stored what could have been broken done to smaller values

2. **Second Normal Form (2NF):** Ensured that all non-key attributes depends on the entire primary keys. 

3. **Third Normal Form (3NF):** Eliminated transitive dependencies by ensuring that all non-key attributes are dependent only on the primary key. The initial design stored lots of 'calculated' values such as winrate which can be derived from the atomic values total_wins/total_games. Since these calculated values are not very resource demanding to calcuate, I decided to remove these values to normalize the database, since after all these calculations queries happens rarely(only during the deployment of the website), and rather I should be focusing more on eliminating redundant data

## Entity-Relationship Diagrams (ERD)

### Overview

The following ERD diagrams illustrate different portions of the database schema, including entities, relationships, and attributes for various aspects of the system.

### Portion 1: HeroCounters 

![HeroCounters ERD](herocountersDB.jpg)

### Overview

This database is actually seperated from the other 2 DBs as initially this DB was used as a seperate project. The database includes several many-to-many relationships between `Hero` entities. These relationships help model various interactions such as matchups, and synergies between heroes. Each relationship is represented by a intemediary table that models this many-many relationship. It also has a one-to-many table that captures the average stats performance of a hero based on the position played

### Tables

**Table:** `vsHeroStats`

- **Purpose:** Captures matchups between 2 `Hero` for the entire game length.

**Table:** `withHeroStats`

- **Purpose:** Captures synergies between 2 `Hero` for the entire game length.

**Table:** `vsLaneStats`

- **Purpose:** Captures matchups between 2 `Hero` in the laning phase.

**Table:** `withLaneStats`

- **Purpose:** Captures synergies between 2 `Hero` in the laning phase.

**Note** vsHeroStats/withHeroStats were seperated into 2 different table instead of combining to 1 as it better represents how the data is used in the website. For example withHeroStats data wont ever be combined with vsHeroStats data and they both have their own seperate table in the website

**Table:** `HeroStats`

- **Purpose:** Captures the performance stats of a hero based on the position played.

**Table:** `HeroTier`

- **Purpose:** Each combination of hero_id + position in HeroStats has one HeroTier. Tier is calculated and can change based on calculation formula so shouldnt be in HeroStats.

**Table:** `Tier`

- **Purpose:** Tier is a look up table for HeroTier 'tier_id' field





### Portion 2: DotaRecaps items 

![HeroCounters ERD](dotarecaps1.jpg)

### Overview
This section has 2 tables similar to HeroCounters portion (HeroStats, Hero) as HeroCounters was a seperate DB.
This table mainly stores 2 things, the many-to-many relationship between a Hero and a Item, and also the laning and the stats of a hero at the 30th minutes

### Tables

**Table:** `Hero`

- **Purpose:** Represents a `Hero` entity.

**Table:** `Item`

- **Purpose:** Represents a item entity.

**Table:** `NeutralItem`

- **Purpose:** Represents a neutral item entity.

**Table:** `ItemStats`

- **Purpose:** Captures how well a `Hero` performs when a item is bought at a specific timing.

**Table:** `NeutralItemStats`

- **Purpose:** Captures how well a `Hero` performs when a neutral item is bought at a specific timing.

**Table:** `LastPatchHero`

- **Purpose:** Represents a `Hero` entity but from the previous patch.

**Table:** `LastPatchItemStats`

- **Purpose:** Captures how well a `Hero` performs when a item is bought at a specific timing for previous patch.

**Table:** `LastPatchNeutralStats`

- **Purpose:** Captures how well a `Hero` performs when a neutral item is bought at a specific timing for previous patch.

**Table:** `LaneHeroStats`

- **Purpose:** Captures the average laning stats of a `Hero` and rank. Used for comparing with user's performance.

**Table:** `HeroStats`

- **Purpose:** Captures the average game stats of a `Hero` and rank. Used for comparing with user's performance.

**Table:** `Rank`

- **Purpose:** Rank table serves as a look-up table. Each combination of hero_id + position in `HeroStats` and `LaneHeroStats` has a field `rank_id`. Helps to maintain data integrity and ease of change in future

### Portion 3: DotaRecaps Profile analysis 

![HeroCounters ERD](dotarecaps2.jpg)

### Overview
This section includes tables meant for storing a user personal analysis data. There is mainly 2 sections here, one portion is the data for the 'profile overview' analysis, while the other section is the data for the 'hero analysis'.

### Tables

**Table:** `User`

- **Purpose:** Represents a User(Person who uses our website) entity.

**Table:** `TopHero` (For profile analysis)

- **Purpose:** Stores the Top heroes the user has used (Each user will have 3 top heroes).

**Table:** `ProfileStat` (For profile analysis)

- **Purpose:** Stores the profile analysis data needed.

**Table:** `PositionStats` (For profile analysis)

- **Purpose:** Stores the data of how well a User has performed on each posiitons.

**Table:** `Ability`

- **Purpose:** Stores the data of a ability.

**Table:** `UserHero`

- **Purpose:** Represents a hero analysed by a User.

**Table:** `HeroMatchStat`

- **Purpose:** Captures general performance stats of a `UserHero`.

**Table:** `HeroLaneStat`

- **Purpose:** Captures laning performance stats of a `UserHero`

**Table:** `MatchUp`

- **Purpose:** Captures the matchup, both enemy and ally, performance of a `UserHero`.

**Table:** `FarmDistribution`

- **Purpose:** Captures the Farm distribution data of a `UserHero`.

**Table:** `KDALocation`

- **Purpose:** Stores the data of where a `UserHero` got kills/deaths/assists.

**Table:** `WardLocation`

- **Purpose:** Stores the ward data of a `UserHero`, specifically location of wards placed by enemy and also by `UserHero`

**Table:** `AbilitiesUsed`

- **Purpose:** Stores the data of the abilities used by a `UserHero`.

**Table:** `MatchOutcome`

- **Purpose:** Shows the match outcome types for a `UserHero`.

**Table:** `LaneOutcome`

- **Purpose:** Shows the lane outcome types for a `UserHero`, including allies' lane outcomes.

**Table:** `Event`

- **Purpose:** Captures events data for a `UserHero`

**Table:** `WardStat`

- **Purpose:** Stores the warding data statistics for a `UserHero`.

**Table:** `ItemPurchased`

- **Purpose:** Stores the data of all ItemPurchased by a `UserHero`.

**Table:** `DamageDistribution`

- **Purpose:** Shows the type of damage recieved/dealt by a `UserHero`.

## Indexes

Indexes will play a crucial role in optimizing the performance, especially for the analysis portion, where large volumes of data are fetched for a single Hero analysis. The indexing strategy differs based on the use case:

- **Profile Analysis:** Non-Clustered Indexes are essential here due to the high volume of data retrieval and rare write operations.
- **Items and HeroCounters:** Non-Clustered indexes are avoided because these tables undergo frequent write operations during daily data fetching, while reads are minimal (static site generation is used).

### **Indexing Strategy**

- **Considerations:** 
  - When creating Composite Indexes (both Clustered and Non-Clustered), prioritize indexing fields used for equality conditions before range conditions.
  - Focus on highly selective fields first to quickly narrow down query results. In general, `steam_id > hero_id > position/role` is the preferred order.
  - The order of columns in composite indexes matters, depending on how you are querying it. 

### **Indexes Used**

**Table:** `UserHero`
- **Index:** A Composite Index on `(steam_id, hero_id)` supports efficient JOIN and WHERE queries. Since a Surrogate key is used, this index is particularly valuable.

**Table:** `MatchUp`
- **Index:** A Clustered Index on `(userhero_id, is_ally, hero_id2)` improves WHERE queries involving `is_ally` and `hero_id2`. Note: The usefulness of including `hero_id2` will be evaluated over time.

**Table:** `KDALocation`
- **Index:** A Non-Clustered Index on `(userhero_id)` supports JOIN queries, given the use of a Surrogate key.

**Table:** `WardLocation`
- **Index:** Similar to `KDALocation`, a Non-Clustered Index on `(userhero_id)` assists with JOIN queries.

**Table:** `AbilitiesUsed`
- **Index:** A UNIQUE CONSTRAINT on `(userhero_id, is_victory, ability_id)` automatically generates an index, which can be leveraged for performance.

**Table:** `MatchOutcome`
- **Index:** A Composite Clustered Index on `(userhero_id, is_victory)` optimizes WHERE queries involving `is_victory`.

**Table:** `LaneOutcome`
- **Index:** A Composite Non-Clustered Index on `(userhero_id, lane, is_victory, is_my_lane)` supports complex queries filtering on these conditions.

