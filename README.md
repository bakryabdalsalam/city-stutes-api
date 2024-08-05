# Custom Country API Plugin

This WordPress plugin provides a custom REST API endpoint to retrieve countries, cities, and districts. The API is designed to work with WooCommerce countries and includes predefined cities and districts for specific countries.

## Installation

1. Upload the `custom-country-api` folder to the `/wp-content/plugins/` directory.
2. Activate the plugin through the 'Plugins' menu in WordPress.

## Usage

The plugin exposes a REST API endpoint to retrieve country data. You can query the endpoint to get all countries, or filter by specific country code, city name, or district name.

### Endpoint


### Query Parameters

- `country_code`: Filter results by a specific country code.
- `city_name`: Filter results by a specific city name within a country.
- `district_name`: Filter results by a specific district name within a city.

### Examples

1. **Get All Countries:**

    ```
    GET /wp-json/custom/v1/countries
    ```

    **Response:**
    ```json
    {
        "AE": { "name": "United Arab Emirates", "cities": ["أبو ظبي", "دبي", "الشارقة", "عجمان", "رأس الخيمة", "أم القيوين", "الفجيرة"] },
        "BH": { "name": "Bahrain", "cities": ["المنامة", "المحرق", "الرفاع", "الحد", "عيسى", "حمد", "البديع"] },
        "KW": { "name": "Kuwait", "cities": ["الكويت", "الفروانية", "الجهراء", "حولي", "الأحمدي", "مبارك الكبير"] },
        "OM": { "name": "Oman", "cities": ["مسقط", "صلالة", "نزوى", "صور", "عبري", "صحار", "البريمي", "رستاق", "خصب"] },
        "SA": { "name": "Saudi Arabia", "districts": { "الرياض": ["المدينة الصناعية الثانية", "جامعة الامام محمد بن سعود الاسلامية", "جامعة الملك سعود"] } },
        "EG": { "name": "Egypt", "cities": ["القاهرة", "الاسكندرية", "الجيزة", "السويس", "المنصورة", "الشرقية", "أسوان", "الأقصر"] }
    }
    ```

2. **Get Data for a Specific Country:**

    ```
    GET /wp-json/custom/v1/countries?country_code=SA
    ```

    **Response:**
    ```json
    {
        "SA": {
            "name": "Saudi Arabia",
            "districts": {
                "الرياض": ["المدينة الصناعية الثانية", "جامعة الامام محمد بن سعود الاسلامية", "جامعة الملك سعود"]
            }
        }
    }
    ```

3. **Get Data for a Specific City in a Country:**

    ```
    GET /wp-json/custom/v1/countries?country_code=SA&city_name=الرياض
    ```

    **Response:**
    ```json
    {
        "SA": {
            "name": "Saudi Arabia",
            "districts": {
                "الرياض": ["المدينة الصناعية الثانية", "جامعة الامام محمد بن سعود الاسلامية", "جامعة الملك سعود"]
            }
        }
    }
    ```

4. **Get Data for a Specific District in a City:**

    ```
    GET /wp-json/custom/v1/countries?country_code=SA&city_name=الرياض&district_name=المدينة الصناعية الثانية
    ```

    **Response:**
    ```json
    {
        "SA": {
            "name": "Saudi Arabia",
            "districts": {
                "الرياض": ["المدينة الصناعية الثانية"]
            }
        }
    }
    ```

### Error Handling

If WooCommerce is not installed or activated, the API will return a 404 error:

```json
{
    "code": "no_woocommerce",
    "message": "WooCommerce is not installed or activated",
    "data": {
        "status": 404
    }
}


You can provide this `README.md` file to your mobile developer to help them understand how to use the custom API you created.
