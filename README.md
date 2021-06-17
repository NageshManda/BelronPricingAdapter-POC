# BelronPricingAdapter-POC

PricingAdapater Integration exposed as an OIC REST Endpoint accept the orders data from Salesforce and creates quote in Oracle CPQ. Once the quote has been sucessfully created in CPQ the relevant data from CPQ (Pricing details) is then returned back to Salesforce.

OIC makes use of the OOTB rest services available from CPQ to create quotes. The CPQ Services used are described below.

## Create Quote
The endpoint used for creating the quote is as detailed below.

End Point : https://<cpqinstance>/rest/v12/<transactionname>/

Method : POST

Request Paylod : 


{
	"transactionLine": {
		"items": [
			{
				"_part_number": "6324BGSH",
				"_price_quantity": "1",
				"_price_book_var_name": "UKFLEET21"
			},
			{
				"_part_number": "6324LGSH5FD",
				"_price_quantity": "1",			
				"_price_book_var_name": "UKFLEET21"
			}
		]
	}	
}

## Update Quote
Currently it is not possible to update the header attributes of quote during the quote creation process so an additional call has to be made to update these header attributes. The endpoint details are as provided below.

End Point : https://<cpqinstance>/rest/v12/<transactionname>/{transaction_id}/actions/cleanSave_t

Method : POST

Request Paylod : 

{
	"documents": {
		"caseNumber": "C-0000000001",
		"description": "UK RSA",
		"customerExcess": {
			"value": 40.0,
			"currency": "GBP"
		},
		"countyRating" : "A",
		"priceEffectiveDate": "2021-06-07",
		"inBranchWarranty": false,
		"discretionaryDiscountAllItems": false,
		"discretionaryDiscountPercentage" : "",
		"motoristName": "Motorist 1",
		"motoristAccountID":"test Motor" ,
		"steered":false,
		"make": "Hyundai",
		"model": "Tucson 5J 2015",
		"modelYear2": "2015",
		"licencePlate": "RA21 4PG",
		"customerID_t": "15",
		"thirdPartyName": "RSA"
	}
}