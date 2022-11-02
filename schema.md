## Database Schema - NoSQL

### Connection String: `mongodb://localhost:27017`, default, no authentication, local only

---

## reddit_stream_comments

```ts
interface RedditComment {
  _id:           string;
  comment_id:    string;
  author:        string;
  text:          string;
  subreddit:     string;
  subreddit_id:  string;
  submission_id: string;
  parent_id:     string;
  created_at:    datetime;
}
```

---

## reddit_stream_submissions

```ts
interface RedditSubmission {
  _id:                    string;
  submission_id:          string;
  title:                  string;
  text:                   string;
  is_self:                boolean;
  subreddit:              string;
  subreddit_id:           string;
  url:                    string;
  url_overridden_by_dest: string;
  crosspost_parent:       string;
  created_at:             datetime;
}
```

---

## subreddit_stats

```ts
interface SubredditStats {
  _id:      string;
  comments: ModeStatistic;
  new:      ModeStatistic;
}

interface ModeStatistic {
  avg_per_second: number;
  last_access:    number;
}
```

---

## twitter_stream

```ts
interface Tweet {
  _id:                    string;
  author_id:              string;
  context_annotations:    ContextAnnotation[];
  conversation_id:        string;
  created_at:             datetime;
  edit_history_tweet_ids: string[];
  entities:               Entities;
  geo:                    Geo;
  lang:                   string;
  text:                   string;
  includes:               Includes;
}

interface ContextAnnotation {
  domain: DataWrapper;
  entity: DataWrapper;
}

interface DataWrapper {
  id:           string;
  name:         string;
  description?: string;
}

interface Entities {
  annotations: Annotation[];
}

interface Annotation {
  start:           number;
  end:             number;
  probability:     number;
  type:            string;
  normalized_text: string;
}

interface Geo {
  place_id: string;
}

interface Includes {
  users:  User[];
  places: Place[];
}

interface Place {
  country_code: string;
  full_name:    string;
  id:           string;
  place_type:   string;
}

interface User {
  created_at:     datetime;
  id:             string;
  name:           string;
  public_metrics: PublicMetrics;
  username:       string;
  verified:       boolean;
}

interface PublicMetrics {
  followers_count: number;
  following_count: number;
  tweet_count:     number;
  listed_count:    number;
}
```

---

## twitter_stream_counts

```ts
interface MinimalTweet {
  _id:        string;
  tweet_id:   string;
  created_at: datetime;
  lang:       string;
  is_stored:  boolean;
}
```

---

## odds_api_keys

```ts
interface OddsAPIKeys {
  _id: string;
  active: boolean;
  api_key: string;
  created_at: datetime;
  remaining: number;
  last_accessed: datetime;
  in_use: datetime;
}
```

---

## odds_`<bookmaker_name>`
The collection name is generated dynamically based on the bookmakers encountered.

```ts
interface BookmakerOdds {
  _id: string;
  sports_key: string;
  sport_title: string;
  home_team: string;
  away_team: string;
  commence_time: datetime;
  last_update: string;
  h2h: OutcomeDatum[];
  spreads: OutcomeDatum[];
  totals: OutcomeDatum[];
}

interface OutcomeDatum {
  saved_at: datetime;
  outcomes: Outcome[];
}

interface Outcome {
  name:  string;
  price: number;
  point?: number;
}
```
