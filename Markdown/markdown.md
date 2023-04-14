---
Title: HTML file
---


## Structural-specification


## Role-definitions

### Role: 

* customerCartManager
* customerCheckoutManager
* customerWalletManager
* customerOrderSender
* customerOrderReceiver
* customerUserAgent
* creditCardEmployee1
* creditCardEmployee2
* creditCardEmployee3
* amazonWorker1
* amazonWorker2
* amazonWorker3
* amazonWorker4
* amazonWorker5
* carrierWorker1
* carrierWorker2
* carrierWorker3
* carrierCustomerCareRepresentative

## Group-specification

* __Id:__ collaboration_group
* __Min:__ 
* __Max:__ 
* __Referred to subgroups:__ none


### Subgroups 0

## Group-specification

* __Id:__ customer_group
* __Min:__ 
* __Max:__ 
* __Referred to subgroups:__ 0


### Roles
#### Role: 

| id | min | max |
|---|---|---|
| customerCartManager | 1 | 1 | 
| customerCheckoutManager | 1 | 1 | 
| customerWalletManager | 1 | 1 | 
| customerOrderSender | 1 | 1 | 
| customerOrderReceiver | 1 | 1 | 
| customerUserAgent | 1 | 1 | 

## Group-specification

* __Id:__ credit_card_group
* __Min:__ 
* __Max:__ 
* __Referred to subgroups:__ 0


### Roles
#### Role: 

| id | min | max |
|---|---|---|
| creditCardEmployee1 | 1 | 1 | 
| creditCardEmployee2 | 1 | 1 | 
| creditCardEmployee3 | 1 | 1 | 

## Group-specification

* __Id:__ amazon_group
* __Min:__ 
* __Max:__ 
* __Referred to subgroups:__ 0


### Roles
#### Role: 

| id | min | max |
|---|---|---|
| amazonWorker1 | 1 | 1 | 
| amazonWorker2 | 1 | 1 | 
| amazonWorker3 | 1 | 1 | 
| amazonWorker4 | 1 | 1 | 
| amazonWorker5 | 1 | 1 | 

## Group-specification

* __Id:__ carrier_group
* __Min:__ 
* __Max:__ 
* __Referred to subgroups:__ 0


### Roles
#### Role: 

| id | min | max |
|---|---|---|
| carrierWorker1 | 1 | 1 | 
| carrierWorker2 | 1 | 1 | 
| carrierWorker3 | 1 | 1 | 
| carrierCustomerCareRepresentative | 1 | 1 | 

## Functional-specification

## Scheme 0 id: customer_sch

### Goal referred to scheme: 0

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| placeOrder |  |  |  |  |  | 

#### Plan 0 referred to goal: placeOrder

| operator | success-rate |
|---|---|
| sequence |  | 

#### Goal referred to plan: 0

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| browseProducts |  |  |  |  |  | 
| addItems |  |  |  |  |  | 
| checkout |  |  |  |  |  | 
| receiveItems |  |  |  |  |  | 

#### Plan 3 referred to goal: checkout

| operator | success-rate |
|---|---|
| sequence |  | 

#### Goal referred to plan: 3

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| payOrder |  |  |  |  |  | 
| sendOrder |  |  |  |  |  | 

## Notification-policy referred to scheme 0
* __Id__: np1
* __Target__: payOrder
* __Condition__: scheme_id(S) &amp; failed(S,payOrder)

* ### Exception-specification __Id__: paymentRefused

    * #### Exception-argument: 

        | id | arity |
        |---|---|
        | balance | 1 | 
    *   #### Raising-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | raisePaymentRefused |  |  |  |  |  |  | 

    *   #### Handling-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | retry |  |  |  |  |  |  | 

## Notification-policy referred to scheme 0
* __Id__: np2
* __Target__: retry
* __Condition__: scheme_id(S) &amp; failed(S,retry)

* ### Exception-specification __Id__: checkoutFailed

    *   #### Raising-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | raiseCheckoutFailed |  |  |  |  |  |  | 

    *   #### Handling-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | cancelOrder |  |  |  |  |  |  | 

## Notification-policy referred to scheme 0
* __Id__: np3
* __Target__: receiveItems
* __Condition__: scheme_id(S) &amp; failed(S,receiveItems)

* ### Exception-specification __Id__: itemsNotReceived

    *   #### Raising-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | raiseItemsNotReceived |  |  |  |  |  |  | 

    *   #### Handling-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | requestRefund |  |  |  |  |  |  | 

## Mission referred to scheme 0
* __Id__: mCustomer1
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ browseProducts
    * __id:__ addItems

## Mission referred to scheme 0
* __Id__: mCustomer3
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ payOrder
    * __id:__ raisePaymentRefused

## Mission referred to scheme 0
* __Id__: mCustomer2
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ checkout
    * __id:__ raiseCheckoutFailed
    * __id:__ retry

## Mission referred to scheme 0
* __Id__: mCustomer4
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ sendOrder

## Mission referred to scheme 0
* __Id__: mCustomer5
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ receiveItems
    * __id:__ raiseItemsNotReceived

## Mission referred to scheme 0
* __Id__: mCustomer6
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ placeOrder
    * __id:__ cancelOrder
    * __id:__ requestRefund

## Scheme 1 id: credit_card_sch

### Goal referred to scheme: 1

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| processPayment |  |  |  |  |  | 

#### Plan 7 referred to goal: processPayment

| operator | success-rate |
|---|---|
| sequence |  | 

#### Goal referred to plan: 7

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| receiveInfo |  |  |  |  |  | 
| takePayment |  |  |  |  |  | 
| sendResult |  |  |  |  |  | 

## Mission referred to scheme 1
* __Id__: mCredit1
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ receiveInfo

## Mission referred to scheme 1
* __Id__: mCredit2
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ takePayment

## Mission referred to scheme 1
* __Id__: mCredit3
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ sendResult

## Scheme 2 id: amazon_sch

### Goal referred to scheme: 2

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| fulfillOrder |  |  |  |  |  | 

#### Plan 11 referred to goal: fulfillOrder

| operator | success-rate |
|---|---|
| sequence |  | 

#### Goal referred to plan: 11

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| receiveOrder |  |  |  |  |  | 
| collectItems |  |  |  |  |  | 
| placeBin |  |  |  |  |  | 
| packageItems |  |  |  |  |  | 
| sendToCarrier |  |  |  |  |  | 

## Mission referred to scheme 2
* __Id__: mAmazon1
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ receiveOrder

## Mission referred to scheme 2
* __Id__: mAmazon2
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ collectItems

## Mission referred to scheme 2
* __Id__: mAmazon3
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ placeBin

## Mission referred to scheme 2
* __Id__: mAmazon4
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ packageItems

## Mission referred to scheme 2
* __Id__: mAmazon5
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ sendToCarrier

## Scheme 3 id: carrier_sch

### Goal referred to scheme: 3

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| shipOrder |  |  |  |  |  | 

#### Plan 17 referred to goal: shipOrder

| operator | success-rate |
|---|---|
| sequence |  | 

#### Goal referred to plan: 17

| id | min | ds | type | ttf | location |
|---|---|---|---|---|---|
| pickItems |  |  |  |  |  | 
| loadTruck |  |  |  |  |  | 
| deliverItems |  |  |  |  |  | 

## Notification-policy referred to scheme 3
* __Id__: np4
* __Target__: deliverItems
* __Condition__: scheme_id(S) &amp; failed(S,deliverItems)

* ### Exception-specification __Id__: itemsLost

    * #### Exception-argument: 

        | id | arity |
        |---|---|
        | recipient | 1 | 
    *   #### Raising-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | raiseItemsLost |  |  |  |  |  |  | 

    *   #### Handling-goal: 

        | id | min | ds | type | ttf | location | when |
        |---|---|---|---|---|---|---|
        | notifyCustomer |  |  |  |  |  |  | 

## Mission referred to scheme 3
* __Id__: mCarrier1
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ pickItems

## Mission referred to scheme 3
* __Id__: mCarrier2
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ loadTruck

## Mission referred to scheme 3
* __Id__: mCarrier3
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ deliverItems
    * __id:__ raiseItemsLost

## Mission referred to scheme 3
* __Id__: mCarrier4
* __Min__: 1
* __max__: 1


* ### Goal
    * __id:__ notifyCustomer


## Normative-specification
### Norm

| id | condition | role | type | mission | time-constraint |
|---|---|---|---|---|---|
| n1 |  | customerCartManager | obligation | mCustomer1 |  | 
| n2 |  | customerCheckoutManager | obligation | mCustomer2 |  | 
| n3 |  | customerWalletManager | obligation | mCustomer3 |  | 
| n4 |  | customerOrderSender | obligation | mCustomer4 |  | 
| n5 |  | customerOrderReceiver | obligation | mCustomer5 |  | 
| n6 |  | customerUserAgent | obligation | mCustomer6 |  | 
| n7 |  | creditCardEmployee1 | obligation | mCredit1 |  | 
| n8 |  | creditCardEmployee2 | obligation | mCredit2 |  | 
| n9 |  | creditCardEmployee3 | obligation | mCredit3 |  | 
| n10 |  | amazonWorker1 | obligation | mAmazon1 |  | 
| n11 |  | amazonWorker2 | obligation | mAmazon2 |  | 
| n12 |  | amazonWorker3 | obligation | mAmazon3 |  | 
| n13 |  | amazonWorker4 | obligation | mAmazon4 |  | 
| n14 |  | amazonWorker5 | obligation | mAmazon5 |  | 
| n15 |  | carrierWorker1 | obligation | mCarrier1 |  | 
| n16 |  | carrierWorker2 | obligation | mCarrier2 |  | 
| n17 |  | carrierWorker3 | obligation | mCarrier3 |  | 
| n18 |  | carrierCustomerCareRepresentative | obligation | mCarrier4 |  | 
