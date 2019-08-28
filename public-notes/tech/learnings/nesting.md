# prefer nesting afterwards


```
/* eslint-disable
  implicit-arrow-linebreak,
  operator-linebreak,
  prefer-template
*/
import {
  curry
} from 'lodash/fp';

import http from '../http';

export default curry(
  (baseUrl) => {
    const materialsUrl = baseUrl('materials');
    const pricingsUrl = baseUrl('pricings');
    const api = {
      get:
        ({id}) =>
          http.get(materialsUrl(id + '/pricings')),
      create:
        ({id}, pricing) =>
          http.post(materialsUrl(id + '/pricings'), pricing),
      update:
        pricing =>
          http.put(pricingsUrl(pricing.id), pricing),
      remove:
        pricing =>
          http.remove(pricingsUrl(pricing.id)),
      upsert:
        pricing => {
          const {materialId, id} = pricing;
          return !id ?
            api.create({id: materialId}, pricing)
            : api.update(pricing);
        },
    };
    return api;
  }
);
```

is better to un nest


```
/* eslint-disable
  implicit-arrow-linebreak,
  operator-linebreak,
  prefer-template
*/
import {
  curry
} from 'lodash/fp';

import http from '../http';

export default curry(
  (baseUrl) => {
    const materialsUrl = baseUrl('materials');
    const pricingsUrl = baseUrl('pricings');

    const get =
      ({id}) =>
        http.get(materialsUrl(id + '/pricings'));

    const create =
      ({id}, pricing) =>
        http.post(materialsUrl(id + '/pricings'), pricing);

    const update =
      pricing =>
        http.put(pricingsUrl(pricing.id), pricing);

    const remove =
      pricing =>
        http.remove(pricingsUrl(pricing.id));

    const upsert =
      pricing => {
        const {materialId, id} = pricing;
        return !id ?
          create({id: materialId}, pricing)
          : update(pricing);
      };

    return {
      get, create, update, remove, upsert
    };
  }
);
```
