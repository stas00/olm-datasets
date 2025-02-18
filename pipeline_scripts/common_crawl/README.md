Follow these steps to pull, process, and push to the Hugging Face hub your very own Common Crawl pretraining dataset, replacing the arguments to suit your needs:

1. `bash download_pipeline_processing_models.sh`
2. `python download_common_crawl.py --common_crawl_snapshots CC-MAIN-2022-33 CC-MAIN-2022-27 --common_crawl_snapshot_offsets 78500 78500 --download_dir=common_crawl_wet_downloads --num_proc=96`
3. `python get_dataset_from_downloads.py --download_dir=common_crawl_wet_downloads --output_dataset_name=Tristan/cc-english --lang_id=en --num_proc=96 --push_to_hub`
4. `python remove_wikipedia_urls.py --input_dataset_name=Tristan/cc-english --output_dataset_name=Tristan/cc-english-no-wikipedia --url_column=url --num_proc=96 --push_to_hub`
5. `python filter_for_only_updated_websites.py --input_dataset_name=Tristan/cc-english-no-wikipedia --output_dataset_name=Tristan/cc-english-updated-no-wikipedia --text_column=text --timestamp_column=timestamp --url_column=url --num_proc=96 --push_to_hub`
6. `python apply_bigscience_filter.py --input_dataset_name=Tristan/cc-english-updated-no-wikipedia --output_dataset_name=Tristan/cc-english-updated-bigscience-filtered-no-wikipedia --lang_id=en --num_proc=96 --push_to_hub`
7. `python deduplicate.py --input_dataset_name=Tristan/cc-english-updated-bigscience-filtered-no-wikipedia --output_dataset_name=Tristan/olm-cc --text_column=text --num_proc=96 --push_to_hub`

