# What is Blob Storage?
- In relational or non-relational db we can store data types like string, int, small json etc. But to store large files like png, jpeg, mp4, or pdf. This files will take alot of space to store on common rows and columns dbs. And it will make the queries much slower.
- So the solution is Blob Storga we can represent all these files such mp4, jpeg etc in to binaries of 0 and 1. Thats why these files are called binary large objects.
- In Blob storgae we store the files and store the metadata on dbs.
- So if users send the img it is first stored in S3 and than its metadata is stored on db. And if users wants to get the img than backend authectcate the user gets user id than get all the blob metadata assiciated with the user id and than send request to s3 to get the image.
- In S3 we create bucker like inkflow-images and than stores the blob into it.
- Bucket
A bucket is like a container for your objects.
For example:
Inkflow-images
- Object
An object is the actual stored file.
diagram-123.png

# Features
1. It is much cheaper option for file storage.
2. It provdes 11 nice durablity, becuase it prodivde redundency to the data.

# presigned URLs:
User
  │
  │ request upload URL
  ↓
Backend
  │
  │ generate presigned URL
  ↓
User
  │
  │ upload directly
  ↓
S3

# Important architecure we can implment using Blob storage.
1. Direct upload to Backend
2. Backend uploads to S3
3. Presigned URL upload ⭐
4. CDN + S3 ⭐
5. Event Processing ⭐
6. Multi-version files
7. Backup architecture
8. Video processing architecture

