# d3-es

[![Greenkeeper badge](https://badges.greenkeeper.io/kiernanmcgowan/d3-es.svg)](https://greenkeeper.io/)

A collection of reusable charts that plug into elasticsearch aggregations. This package is a collection of other plugins. It is possible to just use the sub packages to this library if size is an issue.

## Installing

If you use NPM, `npm install d3-es`. Otherwise, download the [latest release](https://github.com/kiernanmcgowan/d3-es/releases/latest).

## API Reference

### d3_es.geohashgrid()

> More details at [d3-es-geohashgrid](https://github.com/kiernanmcgowan/d3-es-geohashgrid)

Returns a function callable by d3 to render a world chart of locations from the [geohashgrid](https://www.elastic.co/guide/en/elasticsearch/reference/current/search-aggregations-bucket-geohashgrid-aggregation.html) aggregation.

```js
var sample_data = {aggregation: {
  buckets: [{
    'key': 'svz',
    'doc_count': 10964
  }, {
    'key': 'sv8',
    'doc_count': 3198
  }]
}};

var width = 960,
    height = 480;


d3.json('./world-50m.json', function(error, topology) {
  if (error) {
    throw error;
  }

  var geo_chart = d3_es.geohashgrid()
                .data(sample_data.aggregation)
                .topology(topology)
                .width(width).height(height);


  var svg = d3.select('body').append('svg')
    .attr('width', width)
    .attr('height', height)
    .call(geo_chart)
    .selectAll('.pin')
    .attr('r', 5)
    .style('fill', function(d) {
      return d.doc_count > 5000 ? 'red' : 'green';
    });
});
```

## License

MIT