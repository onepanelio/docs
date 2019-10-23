You can persist any file generated during a Job run by saving it into the following folder:

```bash
/onepanel/output
```

You can then [download these files](/jobs/download-output) using the web interface, CLI or SDK.

## Examples

### Save a PyTorch model

```python
import torch.nn as nn

class Model(nn.Module):
    ...
model = Model()
...
# Save model to `/onepanel/output`
torch.save(model.state_dict(), '/onepanel/output/model.pth')
```

### Save a TensorFlow model

```python
import tensorflow as tf

model = tf.keras.models.Sequential([
  ...
])
...
# Save model to `/onepanel/output`
model.save('/onepanel/output/model.h5')
```