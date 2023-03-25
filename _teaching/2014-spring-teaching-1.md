---
title: "RM ICRA robot chassis identification"
collection: teaching
type: "Undergraduate course"
permalink: /teaching/2014-spring-teaching-1
venue: ""
date: 
location: "City, Country"
---

The FCN (Fully Convolutional Network) structure is used, which allows for predicting at any input resolution.

During training, the input is scaled to 416x416 with 3 color channels, resulting in a dimension of 3x416x416. Between each layer, a convolutional layer with a size of 3, stride of 1, and padding of 1 is added, along with a convolutional layer with a size of 2 and stride of 2, to perform convolution and downsampling operations. The output is 48x6x6.

The last layer is the prediction layer, where the category is removed and the coordinate output is added. There are 8 coordinate outputs for the 4 corner points, and an additional confidence output representing the probability that the current grid is the center of the bottom of the object, resulting in a total of 9 dimensions for the output.

The image is divided into 6x6 small grids, and each grid is responsible for predicting whether it is the center of the bottom and predicting the positions of the 4 corner points. The final corner point position is selected from the grid with the highest confidence.

It should be noted that the final network output needs to be limited between 0-1 using the sigmoid function. Therefore, there is a formula for converting between the predicted corner point coordinates and the real image coordinates, as shown in the attached diagram.

The img_scale is the ratio of the image scaling after convolution, which in this case is 416/6.

The loss function has two parts. First, based on the image label, we determine which grid is the center of the object. If the grid is not the center, the loss function for that grid is the square of the confidence value, which means we want to decrease its confidence value. If the grid is the center, the loss function for that grid is the sum of (1- confidence)^2 and the square of the distance between the predicted and real corner points. This means we want to increase the confidence value for that grid and make the predicted corner points as close as possible to the real corner points.


model = Net()
model = torch.load('./6d_car.pt')
model.eval()

dataiter = iter(dataloader)
images, img_path = dataiter.next()

def get_box(output, img_scale):
    output = output[0]
    output = output.numpy()
    c, h, w = output.shape
    boxs = []
    box_scale = 12.0
    for j in range(w):
        for i in range(h):
            if(output[8][i][j] > 0.9):
                box = []
                point1 = [0, 0]
                point1[0] = ((output[0][i][j] - 0.5) * box_scale + j) * img_scale
                point1[1] = ((output[1][i][j] - 0.5) * box_scale + i) * img_scale
                box.append(point1)
                point2 = [0, 0]
                point2[0] = ((output[2][i][j] - 0.5) * box_scale + j) * img_scale
                point2[1] = ((output[3][i][j] - 0.5) * box_scale + i) * img_scale
                box.append(point2)
                point3 = [0, 0]
                point3[0] = ((output[4][i][j] - 0.5) * box_scale + j) * img_scale
                point3[1] = ((output[5][i][j] - 0.5) * box_scale + i) * img_scale
                box.append(point3)
                point4 = [0, 0]
                point4[0] = ((output[6][i][j] - 0.5) * box_scale + j) * img_scale
                point4[1] = ((output[7][i][j] - 0.5) * box_scale + i) * img_scale
                box.append(point4)
                boxs.append(box)
    return boxs

def imshow(imgs, boxs):
    img = imgs[0]
    img = Image.open(os.path.join('./img/', img))
    draw = ImageDraw.Draw(img)
    for index in range(len(boxs)):
        draw.line((boxs[index][0][0],boxs[index][0][1], boxs[index][1][0],boxs[index][1][1]), 'red')
        draw.line((boxs[index][1][0],boxs[index][1][1], boxs[index][2][0],boxs[index][2][1]), 'red')
        draw.line((boxs[index][2][0],boxs[index][2][1], boxs[index][3][0],boxs[index][3][1]), 'red')
        draw.line((boxs[index][3][0],boxs[index][3][1], boxs[index][0][0],boxs[index][0][1]), 'red')
    img = np.array(img)
    plt.imshow(img)
    plt.show()

with torch.no_grad():
    outputs = model(images)
    boxs = get_box(outputs, 69.333)
    imshow(img_path, boxs)

Heading 1
======

Heading 2
======

Heading 3
======