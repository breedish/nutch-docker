## Docker Image

Current configuration of this image consists of components:
	
*	Hadoop 2.4.0
*	HBase 0.94.14
*	Nutch 2.x

##  Base Image

fernandoacorreia/ubuntu-14.04-oracle-java-1.7

## Installation

1. Install [Docker](https://www.docker.com/).

2a. Download automated build from public hub registry `docker pull nutch/nutch_with_hbase_hadoop`

2b. Build from files in this directory:

	$(boot2docker shellinit)
	docker build -t <new name for image> .

## Usage

Start docker
 
	boot2docker up
	$(boot2docker shellinit)

Start an image and enter shell. First command will start image and will print on stdout standard logs.

	IMAGE_PID=$(docker run -i -t  nutch_with_hbase_hadoop)
	docker exec -i -t $IMAGE_PID bash


Nutch is located in /opt/nutch/ and is almost ready to run.
Review configuration in /opt/nutch/conf/ and you can start crawling.

	echo 'http://nutch.apache.org' > seed.txt
	/opt/nutch/bin/nutch inject seed.txt
	/opt/nutch/bin/nutch generate -topN 10 -- this will return batchId
	/opt/nutch/bin/nutch fetch <batchId>
	/opt/nutch/bin/nutch parse <batchId>
	/opt/nutch/bin/nutch updatedb <batchId>
	[...]
