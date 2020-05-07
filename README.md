# Medium-Facenet-Tutorial

Tutorial demonstrating use of Tensorflow, Dlib, and Scikit-learn to create a facial recognition pipeline.

https://hackernoon.com/building-a-facial-recognition-pipeline-with-deep-learning-in-tensorflow-66e7645015b8

--

Notes for AMD GPUs. This is a fork of the originally tutorial to use AMD ROCm's tensorflow.

to run the docker:

```
docker run -v $PWD:/medium-facenet-tutorial \
-e PYTHONPATH=$PYTHONPATH:/medium-facenet-tutorial \
-it --device=/dev/kfd --device=/dev/dri --security-opt seccomp=unconfined --group-add video \
net.tlaloc.us:4443/hackernoon-face \
python3 /medium-facenet-tutorial/medium_facenet_tutorial/train_classifier.py \
--input-dir /medium-facenet-tutorial/output/intermediate \
--model-path /medium-facenet-tutorial/etc/20170511-185253/20170511-185253.pb \
--classifier-path /medium-facenet-tutorial/output/classifier.pkl \
--num-threads 16 \
--num-epochs 25 \
--min-num-images-per-class 10 \
--is-train 
```

Note the switches after `-it` which is `--device=/dev/kfd --device=/dev/dri --security-opt seccomp=unconfined --group-add video`

These are needed to enable access for ROCm inside Docker. For more info see: https://github.com/RadeonOpenCompute/ROCm-docker