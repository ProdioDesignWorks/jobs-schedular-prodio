# jobs-schedular-prodio

### Features

* Minimal overhead. Agenda aims to keep its code base small.
* Mongo backed persistence layer.
* Scheduling with configurable priority, concurrency, and repeating.
* Event backed job queue that you can hook into.
* Optional standalone web-interface dashboard to see jobs with current statuses.

### Example Usage

# 1. This is always the first step to initialize the agenda which will auto sync all pending jobs on server or pm2 restart.

```
const schedular = require('./schedular');
const dbName = "MY_DB";
schedular.initAgenda(dbName);

```

# 2. To Schedule an event/job

* apiUrl - (Required) This is the webhook URL where you want to receive the event at specified or scheduled time interval.
* triggerAt - (Reuired) - It is in the format of "MM/DD/YYYY HH:MM".
* jobId - (Required) - It should be unique, the job will be created with this name.
* Rest fields are just meta data which you will get in return on the webhook URL.

```
let evenObj = {
    "jobTitle": label,
    "jobId": unique_id,
    "apiUrl": _apiUrl,
    "triggerAt": dueDate
}
schedular.setEvent(evenObj);
```

# 3. To cancel already scheduled event

* jobId - (Required) This is the jobId with which the job has been initialized.

```
schedular.cancelEvent(jobId);
```

# 4. To reschedule already scheduled event

* jobId - (Required) This is the jobId with which the job has been initialized.
* jobData - (Required) This is similar to create job JSON Data object which you want to update for the event.

```
schedular.rescheduleEvent(jobId,jobData);
```

### Example Usage (Dashboard)

* You can run directly with `node agenda_dashboard.js` or you can also use `pm2` to run it forever -

```
pm2 start agenda_dashboard.js
```

You will be able to see the dashboard on - `http://localhost:5959/`
