


A django app.


# API
It is a rest API (use django-rest)

## Base API

- Create an account
- Email verification
- Login
- User can be registered
- Password can be changed
- email can be changed (with verification)
- Password can be recovered
- Timezone can be changed
- a listed domains option: Show all incomming traffic or use a allowlist of allowed domains
- There is a json object with simple preferences that can be changed.
- Delete account
- Delete site


## Data Ingress:
as POST data we get a list of objects with the following fields: user, site, metric, value, incr
In a batched manner we:
- Create site objects that do not exist yet for the user. Ignore entries with users that do not exist.
- Increment the count on the respective Count objects

## Data querying

Query by those parameters:
  - start_date
  - end_date
  - site

returns a dict with the aggregated {metric: count} entries




## Modelling

class User:
    id: str (uuid4 or str for legacy users)
    username: str
    email: str
    timezone: int # an utc offset (for now) 
    prefs: dict[str, str]

class Site:
    user_id: str (
    user: User
    domain: str
    allowed_domains: list[str] (default [])
    filter_allowed_domains: bool (default False)
    

class Count
    site: Site
    metric: str
    value: str
    count: int
