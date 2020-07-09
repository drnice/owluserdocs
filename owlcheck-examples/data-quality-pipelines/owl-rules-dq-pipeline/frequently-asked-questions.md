# FAQs

## How to specify OWL database connection properties

{% tabs %}
{% tab title="OwlOptions" %}
```scala
import com.owl.common.options.OwlOptions

val opt = new OwlOptions()
opt.dataset = "<dataset_name>"
opt.runId = "<date>"  // YYYY-MM-DD
opt.load.pguser = "<db_username>"
opt.load.pgpassword = "<db_password>"
opt.load.pghost = "<ip>:<port>/<database_name>"
```
{% endtab %}

{% tab title="Props" %}
```scala
import com.owl.common.Props

val props = new Props()
props.dataset = "<dataset_name>"
props.runId = "<date>"  // YYYY-MM-DD
props.pguser = "<db_username>"
props.pgpassword = "<db_password>"
props.host = "<ip>:<port>/<database_name>"
```
{% endtab %}
{% endtabs %}

## How to verify results

### UI

### Code



