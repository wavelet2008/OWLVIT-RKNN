# OWLVIT

https://huggingface.co/docs/transformers/model_doc/owlvit


https://github.com/AXERA-TECH/OWLVIT-ONNX-AX650-CPP/assets/46700201/51daa50c-170d-4a30-a13b-6e2d659cd05c


<img src="ssd_horse.jpg" height="300" /> <img src="result.jpg" height="300" />

## Get ONNX Model
[README](scripts/README.md)

## Build
```
mkdir build
cd build
```
if x86 onnxruntime
```
cmake -DONNXRUNTIME_DIR=${onnxruntime_dir} -DOpenCV_DIR=${opencv_cmake_file_dir} ..
```
else if ax650
```
cmake -DONNXRUNTIME_DIR=${onnxruntime_dir} -DOpenCV_DIR=${opencv_cmake_file_dir} -DBSP_MSP_DIR=${msp_out_dir} -DBUILD_WITH_AX650=ON -DCMAKE_TOOLCHAIN_FILE=../toolchains/aarch64-none-linux-gnu.toolchain.cmake ..
```
```
make -j4
```
aarch64-none-gnu library:\
[onnxruntime](https://github.com/ZHEQIUSHUI/SAM-ONNX-AX650-CPP/releases/download/ax_models/onnxruntime-aarch64-none-gnu-1.16.0.zip)\
[opencv](https://github.com/ZHEQIUSHUI/SAM-ONNX-AX650-CPP/releases/download/ax_models/libopencv-4.6-aarch64-none.zip)

### Run
```
/opt/test/owlvit # ./main --ienc owlvit-image.axmodel --tenc owlvit-text.onnx -d
 owlvit-post.onnx -v vocab.txt -i ssd_horse.jpg -t text.txt --thread 8
Engine creating handle is done.
Engine creating context is done.
Engine get io info is done.
Engine alloc io is done.
[I][                            init][ 280]: BGR MODEL
[I][              load_image_encoder][  17]: input size 768 768
[I][              load_image_encoder][  29]: image feature len 442368
[I][              load_image_encoder][  32]: pred box cnt  576
[I][               load_text_encoder][ 152]: text feature len 512
[I][                            main][ 120]: image_src [ssd_horse.jpg]
[I][                            main][ 121]: text_src [text.txt]
encode text Inference Cost time : 0.190662s
post Inference Cost time : 0.0550382s
a photo of person 268.899292 20.153463 88.163696 235.837906
a photo of person 428.696014 123.745819 19.836823 55.102310
horse 191.756058 55.418949 229.225601 318.581055
a photo of car 0.000000 98.398750 145.470108 92.571877
a photo of dog 145.470108 203.093140 57.306412 156.490570

root@rk3568:/home/rk3568/rknpu2/examples/OWLVIT/build# ./main  --ienc  owlvit-image.onnx  --tenc  owlvit-text.onnx  -d  owlvit-post.onnx  -v  vocab.txt  -i ssd_horse.jpg  -t text.txt 

inputs: 
        pixel_values: 1 x 3 x 768 x 768[float] 
output: 
        image_embeds: 1 x 24 x 24 x 768 [float] 
          pred_boxes: 1 x 576 x 4 [float] 
[I][              load_image_encoder][  22]: input size 768 768
[I][              load_image_encoder][  32]: image feature len 442368
[I][              load_image_encoder][  36]: pred box cnt  576
[I][               load_text_encoder][ 153]: text feature len 512
[I][                            main][ 170]: image_src [ssd_horse.jpg]
[I][                            main][ 171]: text_src [text.txt]
lanfc stex=text.txt------------------
encode text Inference Cost time : 1.82578s
{
    "test": "cat",
    "texts_feature": "cat.bin",
    "input_ids":[ 49406, 2368, 49407, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}

{
    "test": "dog",
    "texts_feature": "dog.bin",
    "input_ids":[ 49406, 1929, 49407, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}

{
    "test": "bird",
    "texts_feature": "bird.bin",
    "input_ids":[ 49406, 3329, 49407, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}

{
    "test": "person",
    "texts_feature": "person.bin",
    "input_ids":[ 49406, 2533, 49407, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}

{
    "test": "horse",
    "texts_feature": "horse.bin",
    "input_ids":[ 49406, 4558, 49407, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
}

encode imag Inference Cost time : 8.33994s
post Inference Cost time : 0.350379s
dog 171.083221 137.190582 29.378616 30.454895
dog 140.316650 207.184586 57.068985 138.656265
person 270.033417 12.899776 80.040039 216.329422
person 428.823181 123.694420 19.648987 55.240074
horse 171.083221 137.190582 29.378616 30.454895
horse 211.172073 67.156708 210.658859 301.599792

