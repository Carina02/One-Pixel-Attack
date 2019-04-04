We are improving the code. Might release again later.
            conv2d(kernel=3, stride = 1, depth=64, name='layer_conv1').\
	    conv2d(kernel=3, stride = 1, depth=64, name='layer_conv2').\
            max_pool(kernel=2, stride=2).\
	    conv2d(kernel=3, stride = 1, depth=128, name='layer_conv3').\
	    conv2d(kernel=3, stride = 1, depth=128, name='layer_conv4').\
            max_pool(kernel=2, stride=2).\
            conv2d(kernel=3, stride = 1, depth=256, name='layer_conv5').\
	    conv2d(kernel=3, stride = 1, depth=256, name='layer_conv6').\
	    conv2d(kernel=3, stride = 1, depth=256, name='layer_conv7').\
            max_pool(kernel=2, stride=2).\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv8').\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv9').\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv10').\
            max_pool(kernel=2, stride=2).\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv11').\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv12').\
	    conv2d(kernel=3, stride = 1, depth=512, name='layer_conv13').\
            max_pool(kernel=2, stride=2).\
            flatten().\
	    fully_connected(size=2048, name = 'layer_fc1').\
	    fully_connected(size=2048, name = 'layer_fc2').\
            softmax_classifier(num_classes=num_classes, labels=y_true)
