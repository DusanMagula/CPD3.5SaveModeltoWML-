# CPD3.5SaveModeltoWML-

#Below code allows WS users to programatically save model to WS project.  The project is using PySpark Hiring Challenger model.

import os
from ibm_watson_machine_learning import APIClient
url = os.environ['RUNTIME_ENV_APSX_URL']wml_credentials = {
    "instance_id": "openshift",
    "token": os.environ.get("USER_ACCESS_TOKEN"),
    "url": url,
    "version": "3.5"
}client = APIClient(wml_credentials)


client.set.default_project(project_id)


model_name = 'PySpark Hiring Challenger'
software_spec_uid = client.software_specifications.get_uid_by_name('spark-mllib_2.4')
model_props = {
    client.repository.ModelMetaNames.NAME: model_name,
    client.repository.ModelMetaNames.SOFTWARE_SPEC_UID: software_spec_uid,
    client.repository.ModelMetaNames.TYPE: "mllib_2.4"
}
stored_model_details = client.repository.store_model(model=model, pipeline=pipeline, meta_props=model_props, training_data=train_data)
