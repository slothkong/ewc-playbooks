# How to configure the satellite data processing pipeline

## Containers 
Pytroll processing uses three different containers: 
* `trollstalker` → monitors files coming in to local or remote filesystem. 
* `segment gatherer` → collects the segments or messages coming from [trollstalker](https://github.com/pytroll/pytroll-collectors/blob/main/pytroll_collectors/trollstalker.py)(one of the Pytroll collector modules) to one message that contains metadata of all the required files to produce the images 
* `trollflow2` → produces images (using [satpy](https://github.com/pytroll/satpy)) 

## Volumes

The different containers rely on different volumes mounts: 
* `{{ install_dir }}/fci-config/,target=/mnt/config/` → this is where the configuration pipeline that is based on [trollflow2](https://github.com/pytroll/trollflow2) is given to the container. There are different components that run during the processing and configurable with the following files (If you want to see more examples (e.g. FCI, SEVIRI), have a look at the [ewc-config](https://github.com/nordsat/ewc-config) repository in Pytroll.) → 
    * `trollstalker.ini` and `trollstalker_logging.ini` → Configuration file for Trollstalker, which creates posttroll messages for incoming files, and logging config for it. 
    * `segment_gatherer.yaml` → Configuration file for segment_gatherer 
    * `supervisord.conf` → Configuration file for Supervisord, which starts all the processing steps. 
    * `trollflow2.yaml` → Definition of the products to be generated: composites, target areas, file formats, filename patterns. 
* `{{ input_dir }},target=/mnt/input/` → where input images need to be 
* `{{ output_dir }},target=/mnt/output/` → where products, after processing of the input images, will be found 
* `{{ install_dir }}/logs/,target=/mnt/logs` → where logs of the different processing components will be found.
