# -*- mode: ruby -*-
# vi: set ft=ruby :
# Copyright 2013 Google Inc. All Rights Reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

# Usage:
#   $ vagrant up --provider=google
#   $ vagrant destroy

# Customize these global variables
$GOOGLE_PROJECT_ID = "your GOOGLE_PROJECT_ID"
$GOOGLE_JSON_KEY_LOCATION = "location of GOOGLE_JSON_KEY"
$LOCAL_USER = "your local username"
$LOCAL_SSH_KEY = "~/.ssh/id_rsa"

Vagrant.configure("2") do |config|

  config.vm.box = "google/gce"

  config.vm.provider :google do |google, override|
    google.google_project_id = $GOOGLE_PROJECT_ID
    google.google_json_key_location = $GOOGLE_JSON_KEY_LOCATION

    # Override provider defaults
    google.name = "vagrant-gce-jenkins"
    google.image = "centos-7-v20190619"
    google.machine_type = "n1-standard-1"
    google.zone = "us-central1-f"
    google.metadata = {'custom' => 'metadata', 'testing' => 'jenkins'}
    google.tags = ['vagrantbox', 'dev']

    override.ssh.username = $LOCAL_USER
    override.ssh.private_key_path = $LOCAL_SSH_KEY
  end
    config.vm.provision :hostmanager
    config.vm.provision :ansible do |ansible|
      ansible.playbook = "./playbook.yml"
      ansible.extra_vars = {
        hosts: "vagrant-gce-jenkins"
       }
    end
end

