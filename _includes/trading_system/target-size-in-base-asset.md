<!--------------------------------------------- TITLE AND DEFINITION starts -->

{% assign title = "Target Size In Base Asset" %}
{% assign definition = site.data.trading_system.target_size_in_base_asset %}
{% assign preposition = "a" %}
{% assign plural = "s" %}

<!--------------------------------------------- TITLE AND DEFINITION ends -->

{% if include.more == "yes" and include.heading == "more" %}
<details class='detailsCollapsible'><summary class='nobr'>Click to learn more about {{ title | downcase }}{{plural}}
</summary>
{% endif %}

{% if include.heading != "" and include.heading != "more" %}
{{include.heading}} {{title}}
{% endif %}

{% if include.icon != "no" %} 

{% if include.table == "yes" and include.icon != "no" %}
<table class='definitionTable'><tr><td>
{% endif %}

<img src='images/icons/nodes/png{{include.icon}}/{{ title | downcase | replace: " ", "-" }}.png' />

{% if include.table == "yes" and include.icon != "no" %}
</td><td>
{% endif %}

{% endif %}

{% if include.definition == "bold" %}
<strong>{{ definition }}</strong>
{% else %}
{% if include.definition != "no" %}
{{ definition }}
{% endif %}
{% endif %}

{% if include.table == "yes" and include.icon != "no" %}
</td></tr></table>
{% endif %}

{% if include.more == "yes" and include.content == "more" and include.heading != "more" %}
<details class='detailsCollapsible'><summary class='nobr'>Click to learn more about {{ title | downcase }}{{plural}}
</summary>
{% endif %}

{% if include.content != "no" %}

<!--------------------------------------------- CONTENT starts -->

The system supports defining the size of the position in either asset involved in the market: the base asset, or the quoted asset, as per the exchange listing of the market. 

The target size may be defined in one of the two assets only, to avoid inconsistencies. 

The target size is the maximum size the position may achieve. That is, the definition of the target size is used as a cap for the total size of orders that may be placed during the open stage.

If you prefer to define the size of the position denominated in the base asset, then use this node and delete the target size in quoted asset node.

{% include important.html content="Only one target size definition may exist at a time." %}

Even though the definition of the target size is denominated in one of the two assets in the market, the system keeps track of accounts for both assets. That is, performance metrics such as profit loss, ROI, hit ratio, or the annualized rate of return are calculated both based on the base asset and the quoted asset. In fact, metrics are also calculated in a consolidated manner, taking into account both assets at the same time. 

All of this information is made available for multiple contexts, for instance, for each position or the whole episode, through the data structure of the trading engine.

When tracking the results of your trading operation, make sure you refer to the set of accounts that make sense for your trading system. This will all become clearer once you read about the trading engine and the layer managers available on the charts.

{{include.heading}}## Examples

If you are trading the whole balance assigned to the trading system on each position, then your target size will look like this:

```
tradingEngine.current.episode.episodeBaseAsset.balance.value
```

... or...

```
tradingEngine.current.episode.episodeQuotedAsset.balance.value
```

If you are not trading the entire balance on each position, then you may define the target size as a percentage of the balances, or in any other way you may see fit. For such cases, the following formula may be  of use for the close stage target size:

```
tradingEngine.current.strategyOpenStage.stageBaseAsset.sizeFilled.value - tradingEngine.current.strategyOpenStage.stageBaseAsset.feesPaid.value
```

Of course, you may need to adjust the above to use ```stageBaseAsset``` or ```stageQuotedAsset```, as required. In short, the formula returns the amount of the asset obtained by the transactions triggered during the open stage, minus the fees (and slippage, which is already subtracted from the size filled).

<!--------------------------------------------- CONTENT ends -->

{% endif %}

{% if include.more == "yes" and include.content != "more" and include.heading != "more" %}
<details class='detailsCollapsible'><summary class='nobr'>Click to learn more about {{ title | downcase }}{{plural}}
</summary>
{% endif %}

{% if include.adding != "" %}

{{include.adding}} Adding {{preposition}} {{title}} Node

<!--------------------------------------------- ADDING starts -->

To add the {{ title | downcase }} node, select *Add Missing Items* on the parent node menu. 

<!--------------------------------------------- ADDING ends -->

{% endif %}

{% if include.configuring != "" %}

{{include.configuring}} Configuring the {{title}}

<!--------------------------------------------- CONFIGURING starts -->

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

<!--------------------------------------------- CONFIGURING ends -->

{% endif %}

{% if include.starting != "" %}

{{include.starting}} Starting {{preposition}} {{title}}

<!--------------------------------------------- STARTING starts -->

XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX

<!--------------------------------------------- STARTING ends -->

{% endif %}

{% if include.more == "yes" %}
</details>
{% endif %}