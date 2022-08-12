API Reference
=============

.. contents:: Table of contents
   :local:
   :backlinks: none
   :depth: 3


Authentication
~~~~~~~~~~~~~~

Requests to the SmartScan public API are for private usage only.
All endpoints require authentication.

In order to be able to use this API you have to request API **token**.



API Methods
~~~~~~~~~~~


Upload document
+++++++++++++++

.. http:post:: /upload

    Upload file for processing.

    **Example request**:

    .. tabs::

        .. code-tab:: bash

            $ curl --location --request POST 'https://domain.name/upload' \
              --header 'x-api-key: key_token' \
              --form 'file=@"/path/to/your/file/sample_doc.pdf"' \
              --form 'Metadata="{\"org_name\":\"Company Name.\",\"caller_app\":\"Bid Engine\",\"user_id\":\"john-2\",\"file_name\":\"johnd.pdf\",\"file_type\":\"ocr\"}"'

        .. code-tab:: python

            import requests
            import json
            url = "https://domain.name/upload"
            payload={'Metadata': '{"org_name":"Company Name.","caller_app":"Bid Engine","user_id":"john-2","file_name":"johnd.pdf","file_type":"ocr"}'}
            files=[
                ('file',('sample_doc.pdf',open('/path/to/your/file/sample_doc.pdf','rb'),'application/pdf'))
            ]
            headers = {
                'x-api-key': 'token'
            }
            response = requests.request("POST", url, headers=headers, data=payload, files=files)
            print(response.json())

    **Example response**:

    .. sourcecode:: json

        {
            "message": "OK",
            "document_id": "<document_id>.pdf"
        }


Retrieve results based on document id
+++++++++++++++++++++++++++++++++++++

.. http:get:: /get_output

    Get output based on <document_id>.

    **Example request**:

    .. tabs::

        .. code-tab:: bash

            $ curl --location --request GET 'https://domain.name/get_output?document_id=<document_id>.pdf' \
              --header 'x-api-key: token'

        .. code-tab:: python

            import requests
            url = "https://domain.name/get_output?document_id=<document_id>.pdf"
            payload={}
            headers = {
                'x-api-key': 'token'
            }
            response = requests.request("GET", url, headers=headers, data=payload)
            print(response.json())


    **Example response**:

    .. sourcecode:: json

        {
          "message": "OK",
          "output_data": {
            "proposal_info": {
              "annual_mwh": "157897",
              "quote_number": "151926",
              "distribution_company": "distribution_company_name",
              "num_of_electric_accts": "31",
              "prepared_for": "Company Name",
              "supplier_id": "supplier_name"
            },
            "pricing_results": [
              {
                "start_date": "1/1/2020",
                "end_date": "1/1/2021",
                "term_length": "12",
                "adder_price": {
                  "value": "7.66",
                  "unit": "$/MWh"
                },
                "energy": "7.66"
              },
              {
                "start_date": "1/1/2020",
                "end_date": "5/1/2021",
                "term_length": "16",
                "adder_price": {
                  "value": "7.21",
                  "unit": "$/MWh"
                },
                "energy": "7.21"
              },
              {
                "start_date": "1/1/2020",
                "end_date": "1/1/2022",
                "term_length": "24",
                "adder_price": {
                  "value": "7.56",
                  "unit": "$/MWh"
                },
                "energy": "7.56"
              },
              {
                "start_date": "1/1/2020",
                "end_date": "5/1/2022",
                "term_length": "28",
                "adder_price": {
                  "value": "7.32",
                  "unit": "$/MWh"
                },
                "energy": "7.32"
              },
              {
                "start_date": "1/1/2020",
                "end_date": "1/1/2023",
                "term_length": "36",
                "adder_price": {
                  "value": "7.48",
                  "unit": "$/MWh"
                },
                "energy": "7.48"
              }
            ],
            "utility_table": [
              {
                "utility": "utility_company_name",
                "state": "TX",
                "license_number": "PUCT: 00000",
                "tax_notes": null
              }
            ]
          }
        }