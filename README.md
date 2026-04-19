# Accessing Public Drug Data with Python: API Walkthrough

## Objective
Join compound metadata from PubChem with target-oriented annotations from ChEMBL for exploratory research pipelines.

## Example: fetch basic compound descriptors
```python
import requests

cid = 2244
url = f"https://pubchem.ncbi.nlm.nih.gov/rest/pug/compound/cid/{cid}/property/MolecularFormula,MolecularWeight,CanonicalSMILES/JSON"
resp = requests.get(url, timeout=30)
resp.raise_for_status()
props = resp.json()["PropertyTable"]["Properties"][0]
print(props)
```

## Example: ChEMBL molecule lookup
```python
import requests

chembl_id = "CHEMBL25"
url = f"https://www.ebi.ac.uk/chembl/api/data/molecule/{chembl_id}.json"
resp = requests.get(url, timeout=30)
resp.raise_for_status()
print({"name": resp.json().get("pref_name"), "max_phase": resp.json().get("max_phase")})
```

## Interpretation
- PubChem is strong for standardized chemical properties.
- ChEMBL supports target and development context.
- Combined use supports early hypothesis framing.

## Caveats
- API schemas evolve; pin parser logic.
- Identifier mapping across sources can be lossy.

## Next step
Create a reusable ID-mapping utility with retries and schema validation.
