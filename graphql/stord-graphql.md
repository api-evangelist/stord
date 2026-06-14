# Stord GraphQL Schema

## Overview

This conceptual GraphQL schema represents the Stord commerce fulfillment platform API surface. Stord provides omnichannel logistics for DTC and B2B brands, managing orders, inventory, shipments, and returns across a network of 20+ fulfillment nodes.

The schema is derived from Stord's REST API capabilities (documented at https://www.stord.com/integrations), which follows the JSON:API specification. This GraphQL representation offers an alternative interface model covering the same core domains.

## Schema Source

- **Provider**: Stord
- **Base URL**: https://cloud.stord.com
- **Documentation**: https://www.stord.com/integrations
- **Schema File**: stord-schema.graphql
- **Schema Type**: Conceptual (derived from REST API surface)

## Authentication

Stord uses API Key authentication. Each request requires:

- `API-Key` header — API key obtained from your Stord account representative
- `Organisation-ID` header — your organization identifier
- `Network-ID` header — your fulfillment network identifier
- `Facility-ID` header — the specific facility/warehouse identifier

## Core Domains

### Orders

Manage the full order lifecycle from creation through fulfillment. Supports both DTC and B2B order types with omnichannel source tracking.

**Key Types**: `Order`, `OrderDetails`, `OrderStatus`, `OrderType`, `OrderSource`, `Channel`, `ChannelDetails`, `LineItem`, `LineItemDetails`

### Products and Inventory

Track SKUs, barcodes, weights, dimensions, and variants. Manage inventory levels across warehouse locations in real time.

**Key Types**: `Product`, `ProductDetails`, `SKU`, `Barcode`, `Weight`, `Dimensions`, `Variant`, `VariantDetails`, `Inventory`, `InventoryDetails`, `InventoryLevel`, `InventoryLocation`, `InventoryAdjustment`

### Warehousing and Receiving

Manage warehouse locations, zones, and inbound receiving workflows including ASNs (Advanced Shipping Notices).

**Key Types**: `Warehouse`, `WarehouseDetails`, `WarehouseLocation`, `Zone`, `LocationDetails`, `Receiving`, `ReceivingOrder`, `ReceivingLineItem`, `ReceivingStatus`, `ASN`, `ASNDetails`

### Shipments and Carriers

Track outbound shipments, generate labels, and monitor carrier events for packages in transit.

**Key Types**: `Shipment`, `ShipmentDetails`, `ShipmentStatus`, `Label`, `LabelDetails`, `Carrier`, `CarrierDetails`, `TrackingEvent`, `Package`

### Returns

Process returns with line-item granularity, tracking return status through the reverse logistics workflow.

**Key Types**: `Return`, `ReturnDetails`, `ReturnLineItem`, `ReturnStatus`

### Lot and Serial Tracking

Manage lot-controlled and serialized inventory for regulated or high-value goods.

**Key Types**: `Lot`, `LotDetails`, `Serial`, `SerialDetails`

### Platform and Integration

Configure webhooks for event-driven integrations, manage API keys and tokens, and generate operational reports.

**Key Types**: `Webhook`, `WebhookEvent`, `APIKey`, `Token`, `Report`, `ReportDetails`

## Queries

| Query | Description |
|-------|-------------|
| `order(id: ID!)` | Fetch a single order by ID |
| `orders(filter: OrderFilter, page: PageInput)` | List orders with optional filtering |
| `product(id: ID!)` | Fetch a single product/SKU |
| `products(filter: ProductFilter, page: PageInput)` | List products |
| `inventory(locationId: ID!)` | Get inventory at a specific location |
| `inventoryLevels(skuId: ID!)` | Get inventory levels across all locations for a SKU |
| `warehouse(id: ID!)` | Fetch warehouse details |
| `shipment(id: ID!)` | Fetch a shipment by ID |
| `return(id: ID!)` | Fetch a return by ID |
| `asn(id: ID!)` | Fetch an ASN by ID |
| `webhooks` | List configured webhooks |
| `report(id: ID!)` | Fetch a generated report |

## Mutations

| Mutation | Description |
|----------|-------------|
| `createOrder(input: CreateOrderInput!)` | Create a new fulfillment order |
| `cancelOrder(id: ID!)` | Cancel an existing order |
| `createASN(input: CreateASNInput!)` | Create an advanced shipping notice for inbound inventory |
| `adjustInventory(input: InventoryAdjustmentInput!)` | Adjust inventory quantity at a location |
| `createReturn(input: CreateReturnInput!)` | Initiate a return |
| `createWebhook(input: CreateWebhookInput!)` | Register a webhook endpoint |
| `deleteWebhook(id: ID!)` | Remove a webhook registration |
| `generateLabel(shipmentId: ID!)` | Generate a shipping label for a shipment |
| `generateReport(input: ReportInput!)` | Request a new report |
