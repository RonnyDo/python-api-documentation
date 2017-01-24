# Sending Profiles

Sending profiles tell Gophish which SMTP servers to use when sending emails. 

The SMTP endpoint allows you to create, view, and manage Gophish sending profiles.

## Table of Contents

* [Quick Example](#quick-example)
* [Models](#models)
* [Methods](#methods)
* [Examples](#examples)

## Quick Example

This example shows how to retrieve the name of every sending profile in Gophish.

``` python
from gophish import Gophish

api_key = 'API_KEY'
api = Gophish(api_key)

for smtp in api.smtp.get():
    print smtp.name
```

### Models

#### gophish.models.SMTP

A sending profile contains the server address/port, and optional credentials.

##### Attributes

* `id` (int) The smtp ID
* `name` (str) The smtp name
* `html` (str) The smtp HTML
* `text` (str) The smtp HTML
* `modified_date` (optional: datetime.datetime) The scheduled time for smtp launch
* `attachments` (list(models.Attachment)) The optional email attachments

##### Methods

* `__init__(self, **kwargs)` - Returns a new SMTP

Example:

``` python
from gophish.models import *

todo
```

### Methods

#### gophish.api.smtp.get(smtp_id=None)

Gets the details for one or more sending profiles. To get a particular sending profiles, set the ID to the profile ID.

If the `smtp_id` is not set, all sending profiles owned by the current user will be returned.

**Returns**

* If the `smtp_id` is set: `models.SMTP`

* If `smtp_id` is `None`: `list(models.SMTP)`

#### gophish.api.smtp.post(smtp)

Creates a new sending profile. This endpoint requires you to submit a `gophish.models.SMTP` object.

**Returns**

The `gophish.models.SMTP` object that was created.

#### gophish.api.smtp.put(smtp)

Edits an existing sending profile. This endpoint requires you to submit an existing `gophish.models.SMTP` object with its `id` attribute set correctly.

**Returns**

The `gophish.models.SMTP` object that was edited.

#### gophish.api.smtp.delete(smtp_id)

Deletes the sending profile specified by `smtp_id`.

**Returns**

A `gophish.models.Status` message.

### Examples

Here are some examples to show how to use the API.

All of these examples assume the following setup:

``` python
from gophish import Gophish
from gophish.models import *

api_key = 'API_KEY'
api = Gophish(api_key)
```

#### Get All Sending Profiles

``` python
smtp = api.smtp.get()
```

#### Get Single Sending Profile

``` python
smtp = api.smtp.get(smtp_id=1)
```

#### Create New Sending Profile

``` python
smtp = SMTP(name='Test SMTP')

smtp = api.smtp.post(smtp)
print smtp.id
```