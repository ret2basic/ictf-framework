FROM ictf_base

RUN DEBIAN_FRONTEND=noninteractive apt-get install -y  python-pip python-virtualenv python-dev nginx git redis-server build-essential nodejs npm sudo uwsgi uwsgi-plugin-python

COPY ./scoreboard /opt/ictf/scoreboard

WORKDIR /opt/ictf/scoreboard

RUN pip install -r requirements.txt

RUN ansible-playbook provisioning/hephaestus_provisioning/ansible-provisioning.yml --become --extra-vars ICTF_USER="root" --extra-vars ICTF_FRAMEWORK_DIR_HOST="/opt/ictf"  --extra-vars ICTF_API_ADDRESS="database.ictf"

RUN chmod +x ./start.sh

ENTRYPOINT ./start.sh