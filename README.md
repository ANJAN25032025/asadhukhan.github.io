# asadhukhan.github.io
#THE R CODE IS AS FOLLOWS
library(imager)
library(ggplot2)
image_to_matrix = function(image_paths){
  images = lapply(image_paths,
                  function(img)
                  grayscale(load.image(img)))
  matrix_data = sapply(images,as.numeric)
  return(matrix_data)
}
plot_intensity_histogram = function(img){
  img_vector = as.numeric(img)
  hist_data = hist(img_vector,breaks = 10000,plot = FALSE)
  return(hist_data)
}
test_tumor_images = list.files("C:/Users/user/OneDrive/Desktop/BRAIN TUMOR DETECTION/BRAIN WITH TUMOR TEST DATA SET",full.names = TRUE)
test_nontumor_images = list.files("C:/Users/user/OneDrive/Desktop/BRAIN TUMOR DETECTION/BRAIN WITHOUT TUMOR TEST DATA SET",full.names = TRUE)
train_tumor_images = list.files("C:/Users/user/OneDrive/Desktop/BRAIN TUMOR DETECTION/BRAIN WITH TUMOR TRAINING DATA SET",full.names = TRUE)
train_nontumor_images = list.files("C:/Users/user/OneDrive/Desktop/BRAIN TUMOR DETECTION/BRAIN WITHOUT TUMOR TRAINING DATA SET",full.names = TRUE)
test_tumor_matrix = image_to_matrix(test_tumor_images)
save_histogram_image = function(hist_data,filename){
  png(filename)
  hist(hist_data,breaks = 1000,col = "blue",main = "PIXEL INTENSITY HISOGRAM",xlab = "PIXEL INTENSITY",ylab = "FREQUENCY")
  dev.off()
}

dir_path = "C:/Users/user/OneDrive/Desktop/BRAIN TUMOR DETECTION/Histogram image for brain with tumor test data set"
dir.create(dir_path,showWarnings = FALSE)

for (i in seq_along(test_tumor_matrix)){
  hist_data= test_tumor_matrix[[i]]
  filename = paste0(dir_path,"/histogram_",i,".png")
  save_histogram_image(hist_data,filename)
}
for (i in seq_along(test_tumor_matrix)){
  hist_data = plot_intensity_histogram(test_tumor_matrix[[i]])
  print(hist_data$counts)
}
