# counter-app
 counter app created using html tailwind and js

DATA: lv_order_number TYPE BAPI_ALM_ORDER_HEADER_E-ORDERID,
      ls_header       TYPE BAPI_ALM_ORDER_HEADER_E,
      lt_operations   TYPE TABLE OF BAPI_ALM_ORDER_OPERATION_E,
      lt_components   TYPE TABLE OF BAPI_ALM_ORDER_COMPONENT_E,
      lt_partner      TYPE TABLE OF BAPI_ALM_ORDER_PARTNER,
      lt_return       TYPE TABLE OF BAPIRET2.

lv_order_number = '000010000123'. "Example order number; replace with your order

CALL FUNCTION 'BAPI_ALM_ORDER_GET_DETAIL'
  EXPORTING
    number            = lv_order_number
  IMPORTING
    es_header         = ls_header
  TABLES
    et_operations     = lt_operations
    et_components     = lt_components
    et_partner        = lt_partner
    return            = lt_return.

* Display header data
WRITE: / 'Order:', ls_header-orderid,
         'Description:', ls_header-short_text,
         'Status:', ls_header-sys_status.

* Display operations
LOOP AT lt_operations INTO DATA(ls_op).
  WRITE: / 'Operation:', ls_op-activity, ' - ', ls_op-description.
ENDLOOP.

* Display components
LOOP AT lt_components INTO DATA(ls_comp).
  WRITE: / 'Component:', ls_comp-material, 'Qty:', ls_comp-quantity.
ENDLOOP.

* Handle return messages
LOOP AT lt_return INTO DATA(ls_ret).
  WRITE: / 'Message:', ls_ret-message.
ENDLOOP.

