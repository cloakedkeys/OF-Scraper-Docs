# Schema

For the complete, generated list of tables and columns, see [Database tables](../reference/database.md) in the Technical Reference.

## Schemas

The schema may be extended in future versions, but existing columns will remain for backwards compatibility.

Table rebuilds during migration and the Merge Databases menu keep every row, including `is_deleted`. A rebuild runs in one transaction, so if it fails the old table is left intact.

### Labels

| Column | Type |
|---|---|
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `label_id` | `INTEGER` |
| `name` | `VARCHAR` |
| `type` | `VARCHAR` |
| `post_id` | `INTEGER` |
| `model_id` | `INTEGER` |

Unique key: `(post_id, label_id, model_id)`.

### Medias

| Column | Type |
|---|---|
| `model_id` | `INTEGER` |
| `hash` | `VARCHAR` |
| `unlocked` | `BOOL` |
| `duration` | `VARCHAR` |
| `posted_at` | `TIMESTAMP` |
| `created_at` | `TIMESTAMP` |
| `downloaded` | `BOOL` |
| `linked` | `BOOL` |
| `preview` | `INTEGER` |
| `media_type` | `VARCHAR` |
| `api_type` | `VARCHAR` |
| `size` | `INTEGER` |
| `filename` | `VARCHAR` |
| `directory` | `VARCHAR` |
| `link` | `VARCHAR` |
| `post_id` | `INTEGER NOT NULL` |
| `media_id` | `INTEGER` |
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `skip_permanent` | `BOOL` |

Unique key: `(media_id, model_id, post_id)`.

### Messages

| Column | Type |
|---|---|
| `model_id` | `INTEGER` |
| `user_id` | `INTEGER` |
| `created_at` | `TIMESTAMP` |
| `archived` | `BOOLEAN` |
| `paid` | `BOOLEAN` |
| `price` | `INTEGER` |
| `text` | `VARCHAR` |
| `post_id` | `INTEGER NOT NULL` |
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `is_deleted` | `BOOLEAN DEFAULT 0` |
| `group_id` | `VARCHAR` |

Unique key: `(post_id, model_id)`.

### **Posts**

| Column | Type |
|---|---|
| `model_id` | `INTEGER` |
| `created_at` | `TIMESTAMP` |
| `opened` | `BOOLEAN` |
| `stream` | `BOOLEAN` |
| `pinned` | `BOOLEAN` |
| `archived` | `BOOLEAN` |
| `paid` | `INTEGER` |
| `price` | `INTEGER` |
| `text` | `VARCHAR` |
| `post_id` | `INTEGER NOT NULL` |
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `is_deleted` | `BOOLEAN DEFAULT 0` |
| `purchase_type` | `VARCHAR` |
| `mentions` | `VARCHAR` |

Unique key: `(post_id, model_id)`.

### Stories

| Column | Type |
|---|---|
| `model_id` | `INTEGER` |
| `created_at` | `TIMESTAMP` |
| `archived` | `BOOLEAN` |
| `paid` | `INTEGER` |
| `price` | `INTEGER` |
| `text` | `VARCHAR` |
| `post_id` | `INTEGER NOT NULL` |
| `id` | `INTEGER NOT NULL PRIMARY KEY` |

Unique key: `(post_id, model_id)`.

### Models

| Column | Type |
|---|---|
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `model_id` | `INTEGER NOT NULL` |

Unique key: `model_id`.

### Profiles

| Column | Type |
|---|---|
| `username` | `VARCHAR NOT NULL` |
| `user_id` | `INTEGER NOT NULL` |
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `first_seen_at` | `TIMESTAMP` |
| `last_seen_at` | `TIMESTAMP` |

Unique key: `(user_id, username)`.

### Products

Legacy table; nothing writes to it now.

| Column | Type |
|---|---|
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `post_id` | `INTEGER NOT NULL` |
| `model_id` | `INTEGER` |
| `title` | `VARCHAR` |
| `created_at` | `TIMESTAMP` |
| `archived` | `BOOLEAN` |
| `paid` | `INTEGER` |
| `price` | `INTEGER` |
| `text` | `VARCHAR` |

Unique key: `(post_id, model_id)`.

### Others

Legacy table; nothing writes to it now.

| Column | Type |
|---|---|
| `id` | `INTEGER NOT NULL PRIMARY KEY` |
| `post_id` | `INTEGER NOT NULL` |
| `text` | `TEXT` |
| `price` | `VARCHAR` |
| `paid` | `VARCHAR` |
| `archived` | `CHAR` |
| `created_at` | `TEXT` |
| `model_id` | `TEXT` |

Unique key: `(post_id, model_id)`.

### **Schema\_flags**

| Column | Type |
|---|---|
| `flag_name` | `TEXT PRIMARY KEY` |
| `flag_value` | `TEXT` |

Fansly databases also have a row `site` = `fansly`.
