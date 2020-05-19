---
layout: "post"
title: "Get Picklist Values using LWC  "
excerpt: "Get Picklist Values using LWC"
categories: articles
date: "2020-05-01 18:14"
tags: [lwc, salesforce ]
author: pirata21
comments: true
share: true
comments: true
image:
  feature: lwc.jpeg
---

# Get Picklist Values using LWC  

We must to use a wire adapter to get the picklist values for a specified field. To use `getPicklistValues` we should pass the recordTypeId, if our object doesn't has any record type created, we should set the master Record Type(`'012000000000000AAA'`)

## JS
```javascript

import { LightningElement, wire, track } from 'lwc';
import { getPicklistValues } from 'lightning/uiObjectInfoApi'; 
import PIRATE_FIELD from '@salesforce/schema/OpportunityLineItem.Pirate__c'; 

export default class Pirate extends LightningElement {
    masterRecordType = '012000000000000AAA';

    // GET OBJECT INFO
    @wire(
        getPicklistValues, 
        { recordTypeId: '$masterRecordType', fieldApiName: PIRATE_FIELD }
    )
    picklistValues;
}
```

## HTML
```html

<template>
    <lightning-card title="Pirate PicklistValues">
        <template if:true={picklistValues.data}>
           <template for:each={TypePicklistValues.data.values} for:item="item">
              <span key={item.value}>
                {item.label}
              </span>
            </template>
          </template>
    </lightning-card>
</template>
```

