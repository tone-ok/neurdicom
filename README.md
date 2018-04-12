# Welcome to NeurDICOM documentation
NeurDICOM is portable and easy-to-deploy RESTful DICOM and PACS server that allows physicians to use state-of-the-art methods of machine learning and neural networks to make a diagnosis based on medical images processing and interpetating.

## Content
  ### 1. API
  	1.1. Patients
	1.2. Studies
	1.3. Series
	1.4. Instances
	1.5. Plugins

  ### 2. Plugins

## :red_circle: 1. API
- [Users](docs/UsersApiDocs.md)
- [Patients](docs/PatientsApiDocs.md)
- [Studies](docs/StudiesApiDocs.md)
- [Series](docs/SeriesApiDocs.md)
- [Instances](docs/InstancesApiDocs.md)
- [Plugins](docs/PluginsApiDocs.md)
- [Models](docs/ModelsApiDocs.md)
- [DICOM nodes](docs/DicomNodesApiDocs.md)

### 1.1. Patients

**Base URL:** /api

| Resource  | Description  |
| ------------ | ------------ |
| GET /patients  | Find all patients  |
| GET /patients/:id  | Find patient by id  |
| GET /patients/:id/studies  | Find studies for patient  |
| PUT /patients/:id  | Update patient  |
| DELETE /patients/:id  | Delete patient  |

## :green_book: GET /patients
**Description**: Find all patients

## :green_book: GET /patients/:id
**Description**: Find patient by id

## :green_book: GET /patients/:id/studies
**Description**: Find patient's studies

## :green_book: PUT /patients/:id
**Description**: Update patient

## :green_book: DELETE /patients/:id
**Description**: Delete patient

### 1.3 Studies

**Base URL:** /api

| Resource  | Description  |
| ------------ | ------------ |
| GET /studies  | Find all patients  |
| GET /studies/:id  | Find patient by id  |
| GET /studies/:id/series  | Find studies for patient  |
| PUT /studies/:id  | Update study  |
| DELETE /studies/:id  | Delete study  |

## :green_book: GET /studies
**Description**: Find all studies

## :green_book: GET /studies/:id
**Description**: Find study by id

## :green_book: GET /studies/:id/series
**Description**: Find study's series

## :green_book: PUT /studies/:id
**Description**: Update study

## :green_book: DELETE /studies/:id
**Description**: Delete study

### 1.3 Series

**Base URL:** /api

| Resource  | Description  |
| ------------ | ------------ |
| GET /series  | Find all series  |
| GET /series/:id  | Find series by id  |
| GET /series/:id/instances  | Find series' instances  |
| PUT /series/:id  | Update series |
| DELETE /series/:id  | Delete series |

## :green_book: GET /series
**Description**: Find all series

## :green_book: GET /series/:id
**Description**: Find series by id

## :green_book: GET /series/:id/instances
**Description**: Find series' instances

## :green_book: PUT /series/:id
**Description**: Update series

## :green_book: DELETE /series/:id
**Description**: Delete series


## :red_circle: 2. Plugins

Neurdicom provides API for creating plugins to extend the functionality of DICOM files processing. Plugins should be written in Python and packed as ZIP archive. Plugin should have at least two files 'META.json' and 'plugin.py'. 'META.json' describes the plugin, author and main plugin information. Expected strusture of 'META.json' is shown below:

``` json
{
	"plugin_guid": "...",
	"author": "John Doe",
	"name": "hello",
	"info": "Print hello greeting",
	"help": "To greet say 'Hello'",
	"params": {
		"name": {
			"type": "text"
		}
	}
}
```
Field "params" list all parameters which plugin expects. Each "params" field has one of several options "type", "isarray", "values", "isnull". Field "type" is obligatory and takes one of the following values:
```json
[
	"text",
	"int",
	"double"
]
```
Fields "isarray", "isnull" are boolearn or nullable. Nullable value are is considered as false.  
Plugin should have a public "Plugin" class. "Plugin" class should have at least three of the following methods "init", "process" and "destory". Example of "Plugin" class is shown below:
```python
class Plugin:
    def init(self):
        print('Init method called')

    def process(self, ds: Dataset = None, *args, **kwargs):
        print('Hello,', kwargs['name'], '!')
        return {
            'greeting': 'Hello, %s!' % kwargs['name']
        }

    def destroy(self):
        print('Destroy method called')
```
