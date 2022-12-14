# Yelp-Business-Rating-Prediction

In this project I will be attempting to classify Yelp Reviews into 1 star or 5 star categories based off the text content in the reviews. 

Each observation in this dataset is a review of a particular business by a particular user.

The "stars" column is the number of stars (1 through 5) assigned by the reviewer to the business. (Higher stars is better.) In other words, it is the rating of the business by the person who wrote the review.

The "cool" column is the number of "cool" votes this review received from other Yelp users.

All reviews start with 0 "cool" votes, and there is no limit to how many "cool" votes a review can receive. In other words, it is a rating of the review itself, not a rating of the business.

The "useful" and "funny" columns are similar to the "cool" column.

# About the Data

The data is a detailed dump of Yelp reviews, businesses, users, and checkins for the Phoenix, AZ metropolitan area. 
Business
{
  'type': 'business',
  'business_id': (encrypted business id),
  'name': (business name),
  'neighborhoods': [(hood names)],
  'full_address': (localized address),
  'city': (city),
  'state': (state),
  'latitude': latitude,
  'longitude': longitude,
  'stars': (star rating, rounded to half-stars),
  'review_count': review count,
  'categories': [(localized category names)]
  'open': True / False (corresponds to permanently closed, not business hours),
}
Review
{
  'type': 'review',
  'business_id': (encrypted business id),
  'user_id': (encrypted user id),
  'stars': (star rating),
  'text': (review text),
  'date': (date, formatted like '2012-03-14', %Y-%m-%d in strptime notation),
  'votes': {'useful': (count), 'funny': (count), 'cool': (count)}
}
User
Some user profiles are omitted from the data because they have elected not to have public profiles. Their reviews may still be in the data set if they are still visible on Yelp.

{
  'type': 'user',
  'user_id': (encrypted user id),
  'name': (first name),
  'review_count': (review count),
  'average_stars': (floating point average, like 4.31),
  'votes': {'useful': (count), 'funny': (count), 'cool': (count)}
}
Checkin
If there are no checkins for a business, the entire record will be omitted.

{
  'type': 'checkin',
  'business_id': (encrypted business id),
  'checkin_info': {
        '0-0': (number of checkins from 00:00 to 01:00 on all Sundays),
        '1-0': (number of checkins from 01:00 to 02:00 on all Sundays), 
        ... 
        '14-4': (number of checkins from 14:00 to 15:00 on all Thursdays),
        ...
        '23-6': (number of checkins from 23:00 to 00:00 on all Saturdays)
  } # if there was no checkin for an hour-day block it will not be in the dict
}
Testing Data
The testing data format is the same as the training data, except that several fields have been removed. Identifiers are consistent between the test set and the training set. The test set's user and business files only contain the records that cannot already be found in the training set. Information from the training set was not duplicated into the testing set; please cross reference both data sets to make your predictions. Although these users and businesses may not be new to Yelp, they are new to this data set, and don't have as much information attached to them.

Review
Since you are trying to predict how a user will rate a business, the only information in a Review object is the user_id and business_id. The CSV file you submit should contain a predicted rating for every (user_id, business_id) pair in this file.

Business
The stars field has been removed from the Business object. If a business object is included in the testing set, that means there were no reviews of this business included in the training set. The test set may not ask you to predict a rating for as many reviews as review_count.

User
The average_stars and votes fields have been removed from the User object. If a user object is included in the testing set, that means there were no reviews by this user included in the training set. The test set may not ask you to predict a rating for as many reviews as review_count.

Checkin
The checkin format is the same as in the training set.
