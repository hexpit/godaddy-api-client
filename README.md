# GoDaddy Domains API Client

API client for [GoDaddy Domains](https://developer.godaddy.com) 

## Requirements

PHP 5.4.0 and later

## Installation & Usage
### Composer

To install the bindings via [Composer](http://getcomposer.org/), add the following to `composer.json`:

```php
{
  "require" : {
    "gellu/godaddy-api-client" : "1.*"
  }
}
```

Then run `composer install`


## Example - Domain purchase

```php
<?php
require_once(__DIR__ . '/vendor/autoload.php');

const API_KEY = 'dKYQMqaKm5qZ_BL4bc9pSWi9h3x2cRnW3hq';
const API_SECRET = '3YFoJRdwcC7UAocLb4D8ZV';

$domain 			= 'test-domain.com';
$domainPeriod 		= 1;
$domainAutoRenew	= false;
$domainTLD 			= 'pl';
$contact 			= [
	'name'			=> 'John',
	'surname'		=> 'Doe',
	'email'			=> 'john.doe@test-domain.com',
	'phone'			=> '+48.111111111',
	'organization'	=> 'Corporation Inc.',
	'street'		=> 'Street Ave. 666',
	'city'			=> 'New City',
	'country'		=> 'PL',
	'postal-code'	=> '11-111',
	'state'			=> 'state of art'
];

$configuration = new \GoDaddyDomainsClient\Configuration();
$configuration->addDefaultHeader("Authorization", "sso-key ". API_KEY .":". API_SECRET);
$configuration->setDebug(true);

$apiClient = new \GoDaddyDomainsClient\ApiClient($configuration);
$apiInstance = new \GoDaddyDomainsClient\Api\VdomainsApi($apiClient);

$agreement = $apiInstance->getAgreement($domainTLD, false);
$agreementKeys = [$agreement[0]->getAgreementKey()];

$domainPurchase = new \GoDaddyDomainsClient\Model\DomainPurchase();
$domainPurchase->setDomain($domain);

$domainPurchaseConsent = new \GoDaddyDomainsClient\Model\Consent();
$domainPurchaseConsent->setAgreementKeys($agreementKeys);
$domainPurchaseConsent->setAgreedBy($contact['name'] . ' ' . $contact['surname']);
$domainPurchaseConsent->setAgreedAt(date("Y-m-d\TH:i:s\Z"));
$domainPurchase->setConsent($domainPurchaseConsent);

$domainContactAdmin = new \GoDaddyDomainsClient\Model\Contact();
$domainContactAdmin->setNameFirst($contact['name']);
$domainContactAdmin->setNameLast($contact['surname']);
$domainContactAdmin->setEmail($contact['email']);
$domainContactAdmin->setPhone($contact['phone']);
$domainContactAdmin->setOrganization($contact['organization']);

$domainContactAdminAddressMailing = new \GoDaddyDomainsClient\Model\Address();
$domainContactAdminAddressMailing->setAddress1($contact['street']);
$domainContactAdminAddressMailing->setCity($contact['city']);
$domainContactAdminAddressMailing->setCountry($contact['country']);
$domainContactAdminAddressMailing->setPostalCode($contact['postal-code']);
$domainContactAdminAddressMailing->setState($contact['state']);

$domainContactAdmin->setAddressMailing($domainContactAdminAddressMailing);

$domainPurchase->setContactAdmin($domainContactAdmin);
$domainPurchase->setContactBilling($domainContactAdmin);
$domainPurchase->setContactRegistrant($domainContactAdmin);
$domainPurchase->setContactTech($domainContactAdmin);
$domainPurchase->setPeriod(1);
$domainPurchase->setRenewAuto(false);

$purchase = $apiInstance->purchase($domainPurchase);
```

## Documentation For Models

 - [Address](docs/Model/Address.md)
 - [Consent](docs/Model/Consent.md)
 - [Contact](docs/Model/Contact.md)
 - [DNSRecord](docs/Model/DNSRecord.md)
 - [DNSRecordCreateType](docs/Model/DNSRecordCreateType.md)
 - [DNSRecordCreateTypeName](docs/Model/DNSRecordCreateTypeName.md)
 - [Domain](docs/Model/Domain.md)
 - [DomainAvail](docs/Model/DomainAvail.md)
 - [DomainAvailableResponse](docs/Model/DomainAvailableResponse.md)
 - [DomainContacts](docs/Model/DomainContacts.md)
 - [DomainDetail](docs/Model/DomainDetail.md)
 - [DomainPurchase](docs/Model/DomainPurchase.md)
 - [DomainPurchaseResponse](docs/Model/DomainPurchaseResponse.md)
 - [DomainRenew](docs/Model/DomainRenew.md)
 - [DomainSuggestion](docs/Model/DomainSuggestion.md)
 - [DomainSummary](docs/Model/DomainSummary.md)
 - [DomainTransferIn](docs/Model/DomainTransferIn.md)
 - [DomainUpdate](docs/Model/DomainUpdate.md)
 - [Error](docs/Model/Error.md)
 - [ErrorField](docs/Model/ErrorField.md)
 - [ErrorLimit](docs/Model/ErrorLimit.md)
 - [IdentityDocumentCreate](docs/Model/IdentityDocumentCreate.md)
 - [JsonDataType](docs/Model/JsonDataType.md)
 - [JsonProperty](docs/Model/JsonProperty.md)
 - [JsonSchema](docs/Model/JsonSchema.md)
 - [LegalAgreement](docs/Model/LegalAgreement.md)
 - [PrivacyPurchase](docs/Model/PrivacyPurchase.md)
 - [RealNameValidation](docs/Model/RealNameValidation.md)
 - [TldSummary](docs/Model/TldSummary.md)


This PHP package is automatically generated by the [Swagger Codegen](https://github.com/swagger-api/swagger-codegen) project:

- API version: 2.4.8
- Build date: 2016-09-01T15:18:33.475Z
- Build package: class io.swagger.codegen.languages.PhpClientCodegen

