## TFSecured

Small library for encryption/decryption tensorflow proto models (*.pb).

## Usage 

C++ Usage (see [TFPredictor.mm](https://github.com/dneprDroid/TFSecured/blob/master/iosDemo/TFSecured-iOS/tf/predict/TFPredictor.mm)):

```cpp

    tensorflow::GraphDef graph;
    // Decryption: 
    auto status = tfsecured::GraphDefDecryptAES(path,         // path to *.pb file (frozen graph)
                                                &graph,
                                                keyUnhashed); // AES base64 key
    if (!status.ok()) {
        std::cout << status.error_message() << std::endl;
        return;
    }
    
    // Create session :
    std::unique_ptr<Session> session(NewSession(options));
    status = session->Create(*graph);
    
    // Run session ....
```


Encrypt model via python script (see [encrypt_model.py](https://github.com/dneprDroid/TFSecured/blob/master/python/encrypt_model.py)):

```bash
$ python encrypt_model.py <INPUT_PB_MODEL>  \
                          <OUTPUT_PB_MODEL> \  
                          <KEY>                # optional, generated randomly by script 

```