# API 说明

### ROSTER
  1. https://api.aminer.org/api/roster/:id/offset/:offset/size/:size?rev=1
	  * id: roster的id, size: 最大为100, rev: 返回数据倒排，默认顺序新添加的专家在最后
# Routes
# This file defines all application routes (Higher priority routes first)
# ~~~~

# Develop Notes:
#

# Home page
GET           /                                                                                                          controllers.ApplicationController.index
GET           /favicon.ico                                                                                               controllers.Assets.at(path="/public", file="favicon.ico")

# APIsx
# Index Page
GET           /api/hot_topic                                                                                             controllers.index.IndexController.getHotTopics
PUT           /api/hot_topic                                                                                             controllers.index.IndexController.updateHotTopics()
GET           /api/stats                                                                                                 controllers.index.IndexController.getDBStats
GET           /api/stars/daily                                                                                           controllers.index.IndexController.todaysStar
GET           /api/blacklist                                                                                             controllers.index.IndexController.blackListStatus

GET           /api/rec-rosters                                                                                           controllers.index.IndexController.recRoster

GET           /api/geo/user                                                                                              controllers.index.IndexController.userLocation

# User
GET           /api/user/me                                                                                               controllers.user.UserController.getMe
GET           /api/user/:id                                                                                              controllers.user.UserController.getUserById(id)
PATCH         /api/user/:id                                                                                              controllers.user.UserController.updateUserProfile(id)
POST          /api/user/:uid/tag/:tag                                                                                    controllers.user.UserController.addUserTag(uid, tag)
DELETE        /api/user/:uid/untag/:tag                                                                                  controllers.user.UserController.removeUserTag(uid, tag)

PUT           /api/user/bind/:id                                                                                         controllers.user.UserController.bindProfile(id)

POST          /api/user/bind                                                                                             controllers.user.UserController.bindBlankProfile

PUT           /api/user/unbind                                                                                           controllers.user.UserController.unbindProfile

GET           /api/user/check/:email                                                                                     controllers.user.UserController.checkRegedEmail(email)
GET           /api/user/check/src/:src/email/:email                                                                      controllers.user.UserController.checkRegedEmailWithSrc(src, email)

GET           /api/user/bind/status                                                                                      controllers.user.UserController.getBindInfo


GET           /api/user/mail/template/list/:src                                                                          controllers.user.UserMailTemplateController.listTemplates(src)
GET           /api/user/mail/template/:src/:category                                                                     controllers.user.UserMailTemplateController.getTemplate(src, category)
PUT           /api/user/mail/template/:src/:category                                                                     controllers.user.UserMailTemplateController.setTemplate(src, category)
DELETE        /api/user/mail/template/:src/:category                                                                     controllers.user.UserMailTemplateController.rmTemplate(src, category)

# User Role Operation
#TODO add
#GET           /api/user/role/:uid                     # get one person's role information , include all role labels, subrole labels and all related permissions

POST          /api/user/role/invoke                                                                                      controllers.user.RoleController.invoke()
POST          /api/user/role/revoke                                                                                      controllers.user.RoleController.revoke()

GET           /api/user/role/perms                                                                                       controllers.user.RoleController.listUserPerm

# Role Management
#GET          /api/role/:rlid                         # get role by id
#GET           /api/user/role/getroledetail/:roleLabel      controllers.user.RoleController.getRoleDetail(roleLabel: String)
#POST          /api/role/add                           controllers.user.RoleController.addRole()
GET           /api/role/offset/:offset/size/:size                                                                        controllers.user.RoleController.listRole(offset: Int, size: Int)

GET           /api/user/role/list/:role/offset/:offset/size/:size                                                        controllers.user.RoleController.listUsersByRole(role, offset: Int, size: Int)

# The follow lines shall merged into one api
# POST        /api/role/update                       #TODO, update one role's information
#POST          /api/user/role/updatedesc/:roleLabel/:desc   controllers.user.RoleController.updateDesc(roleLabel: String, desc: String)
#POST          /api/user/role/addsubrole/:roleLabel/:subRoleLabel     controllers.user.RoleController.addSubRole(roleLabel: String, subRoleLabel: String)
#POST          /api/user/role/removesubrole/:roleLabel/:subRoleLabel     controllers.user.RoleController.removeSubRole(roleLabel: String, subRoleLabel: String)
#POST          /api/user/role/updatePerm/:roleLabel/:permTar/:opr/:value     controllers.user.RoleController.updatePerm(roleLabel: String, permTar: String, opr: String, value: Boolean)

GET           /api/user/src/list/:src/offset/:offset/size/:size                                                          controllers.user.RoleController.listUsersBySrc(src, offset: Int, size: Int)

GET           /api/user/token/search/:id                                                                                 controllers.user.SearchTokenController.getSearchToken(id)
DELETE        /api/user/token/search/:id                                                                                 controllers.user.SearchTokenController.rmSearchToken(id)
POST          /api/user/token/search/name/:name/:dl                                                                      controllers.user.SearchTokenController.addSearchToken(name: String, dl: Long)
GET           /api/user/token/search/offset/:offset/size/:size                                                           controllers.user.SearchTokenController.listSearchTokens(offset: Int, size: Int)


# Auth
POST          /api/auth/signup                                                                                           controllers.auth.AuthorizationController.signUp
POST          /api/auth/signout                                                                                          controllers.auth.AuthorizationController.signOut
POST          /api/auth/signin                                                                                           controllers.auth.CredentialsAuthController.authenticate
POST          /api/auth/credentials                                                                                      controllers.auth.CredentialsAuthController.authenticate
POST          /api/auth/social/ckcest                                                                                    controllers.auth.CAESocialAuthController.authenticate
POST          /api/auth/social/wechat                                                                                    controllers.auth.WechatSocialAuthController.authenticate
DELETE        /api/auth/social/wechat                                                                                    controllers.auth.WechatSocialAuthController.deauthenticate
POST          /api/auth/social/:provider                                                                                 controllers.auth.SocialAuthController.authenticate(provider)
GET           /api/auth/ckcestauth/signin                                                                                controllers.auth.CAESocialAuthController.authenticateByCas

POST          /api/auth/update/passwd                                                                                    controllers.auth.AuthorizationController.updatePasswordByOldPassword
POST          /api/auth/update/token                                                                                     controllers.auth.AuthorizationController.updatePasswordByToken
POST          /api/auth/update/forgot                                                                                    controllers.auth.AuthorizationController.forgotPassword
POST          /api/auth/update/verify                                                                                    controllers.auth.AuthorizationController.tokenVerification
POST          /api/auth/update/verify/resend                                                                             controllers.auth.AuthorizationController.resendInitMessage

POST          /api/auth/token/retrieve                                                                                   controllers.auth.AuthorizationController.tokenRetrieve

## Auth Sp
POST          /api/auth/update/test/accs/:email                                                                          controllers.auth.AuthorizationController.updatePasswordForTestAccount(email)

#shenzhenauth authentication
GET           /api/auth/shenzhenauth/szccassignin                                                                        controllers.auth.ShenzhenSocialAuthController.szcCasSignIn
GET           /api/auth/shenzhenauth/szulsignin                                                                          controllers.auth.ShenzhenSocialAuthController.szulSignIn
POST          /api/auth/shenzhenauth/signin                                                                              controllers.auth.ShenzhenSocialAuthController.signIn

# Social
GET           /api/social/following/size/:uid                                                                            controllers.social.SocialNetworkController.getUserFollowingSize(uid:String)
GET           /api/social/following/list/:uid/offset/:offset/size/:size                                                  controllers.social.SocialNetworkController.getUserFollowingList(uid:String, offset: Int , size: Int )

GET           /api/social/follower/size/uid/:uid                                                                         controllers.social.SocialNetworkController.getUserFollowerSize(uid:String)
GET           /api/social/follower/list/uid/:uid/offset/:offset/size/:size                                               controllers.social.SocialNetworkController.getUserFollowerList(uid:String, offset: Int , size: Int )

GET           /api/social/follower/size/aid/:aid                                                                         controllers.social.SocialNetworkController.getPersonFollowerSize(aid:String)
GET           /api/social/follower/list/aid/:aid/offset/:offset/size/:size                                               controllers.social.SocialNetworkController.getPersonFollowerList(aid:String, offset: Int , size: Int )


POST          /api/social/:aid/follow                                                                                    controllers.social.SocialNetworkController.followPersonByUidAid(aid:String)
DELETE        /api/social/:aid/follow                                                                                    controllers.social.SocialNetworkController.unfollowPersonByUidAid(aid:String)

GET           /api/social/status/following/:pid                                                                          controllers.social.SocialNetworkController.userIsFollowing(pid:String)

POST          /api/social/:aid/tag/:tid                                                                                  controllers.social.SocialNetworkController.tagPersonByUidAid(aid:String, tid:Int)
DELETE        /api/social/:aid/tag/:tid                                                                                  controllers.social.SocialNetworkController.untagPersonByUidAid(aid:String, tid:Int)

GET           /api/social/tag/uid/:uid/size                                                                              controllers.social.SocialNetworkController.getUserTaggingSizes(uid:String)
GET           /api/social/tag/uid/:uid/tid/:tid/offset/:offset/size/:size                                                controllers.social.SocialNetworkController.getUserTaggingList(uid:String,tid:Int,offset:Int,size:Int)
GET           /api/social/recommend/uid/:uid                                                                             controllers.social.SocialNetworkController.getExpertsRecommendation(uid:String)
GET           /api/social/recommendpubs/uid/:uid                                                                         controllers.social.SocialNetworkController.getPubsRecommendation(uid:String)


# Social Timeline

GET           /api/social/tl/offset/:offset/size/:size                                                                   controllers.social.TimelineController.getUserSubscribe(offset:Int,size:Int)
DELETE        /api/social/tl/:tlid                                                                                       controllers.social.TimelineController.hideFromTimeline(tlid)

POST          /api/social/tl/:tlid/like                                                                                  controllers.social.TimelineController.likeElementOfTimeline(tlid)
DELETE        /api/social/tl/:tlid/like                                                                                  controllers.social.TimelineController.unlikeElementOfTimeline(tlid)

POST          /api/social/pub/:pid/like                                                                                  controllers.pub.PublicationCommentController.starOnePub(pid)
DELETE        /api/social/pub/:pid/like                                                                                  controllers.pub.PublicationCommentController.unstarOnePub(pid)

GET           /api/social/pub/changelog                                                                                  controllers.social.TimelineController.getPubUpdate
GET           /api/social/pub/changelog/sz                                                                               controllers.social.TimelineController.getSzPubUpdate

# list starred/bookmarked
GET           /api/social/pub/likded/offset/:offset/size/:size                                                           controllers.pub.PublicationCommentController.listStarringPubs(offset:Int, size:Int)

# Comments

POST          /api/comment/:_type/:id                                                                                    controllers.social.CommentController.addComment(id, _type)
DELETE        /api/comment/:_type/cmid/:id                                                                               controllers.social.CommentController.deleteComment(id, _type)
GET           /api/comment/:_type/:id/offset/:offset/size/:size                                                          controllers.social.CommentController.listComments(id, _type, offset:Int,size:Int)
POST          /api/comment/:_type/:id/like                                                                               controllers.social.CommentController.likeComment(id, _type)
DELETE        /api/comment/:_type/:id/like                                                                               controllers.social.CommentController.unlikeComment(id, _type)

#Search
GET           /api/search/person/20160603/and                                                                            controllers.search.PersonSearchController.searchPeopleWithPolicy20160603And
GET           /api/search/person/20160603/or                                                                             controllers.search.PersonSearchController.searchPeopleWithPolicy20160603Or

GET           /api/search/person                                                                                         controllers.search.PersonSearchController.searchPersonWithDSL
GET           /api/search/person/agg                                                                                     controllers.search.PersonSearchController.searchPersonAgg
GET           /api/search/person/geo                                                                                     controllers.search.PersonSearchController.searchPersonGeo
GET           /api/search/person/multi                                                                                   controllers.search.PersonSearchController.searchPersonMultiKeywords
GET           /api/search/person/advanced                                                                                controllers.search.PersonSearchController.searchPersonAdvc
GET           /api/search/person/advanced/agg                                                                            controllers.search.PersonSearchController.searchPersonAdvcAgg
GET           /api/search/person/advanced/geo                                                                            controllers.search.PersonSearchController.searchPersonAdvcGeo

GET           /api/search/person/ego                                                                                     controllers.search.PersonSearchController.searchExpertNetWithDSL

GET           /api/search/person/dump.csv                                                                                controllers.search.PersonSearchController.searchPersonWithDSLDumpAsCSV
GET           /api/search/person/advanced/dump.csv                                                                       controllers.search.PersonSearchController.searchPersonAdvcDumpAsCSV

GET           /api/search/pub                                                                                            controllers.search.PubSearchController.searchPub
GET           /api/search/pub/advanced                                                                                   controllers.search.PubSearchController.searchPubAdvc

GET           /api/search/activity                                                                                       controllers.search.ActivitySearchController.searchActivity

GET           /api/search/suggest/gen/:query                                                                             controllers.search.SuggestController.suggest(query)
GET           /api/search/suggest/org/:query                                                                             controllers.search.SuggestController.suggestOrg(query)
GET           /api/search/suggest/person/:query                                                                          controllers.search.SuggestController.suggestPerson(query)
GET           /api/search/suggest/topic/:query                                                                           controllers.search.SuggestController.suggestTopic(query)
GET           /api/search/suggest/pub/:query                                                                             controllers.search.SuggestController.suggestPub(query)
GET           /api/search/suggest/inst/:query                                                                            controllers.search.SuggestController.suggestInst(query)
GET           /api/search/suggest/activity/:query                                                                        controllers.search.SuggestController.suggestActivity(query)

GET           /api/search/suggest/venue/:query                                                                           controllers.search.VenueSearchController.suggestVenue(query)

GET           /api/search/pub/aff/:id/agg                                                                                controllers.search.PubSearchInAffController.aggPubInAff(id)
GET           /api/search/pub/aff/:id                                                                                    controllers.search.PubSearchInAffController.searchPubInAff(id)

GET           /api/search/pub/inst/:id/agg                                                                               controllers.search.PubSearchInInstController.searchPubsAggregationInInstitution(id)
GET           /api/search/pub/inst/:id                                                                                   controllers.search.PubSearchInInstController.searchPubsInInstitution(id)

GET           /api/search/roster/:id/experts                                                                             controllers.search.RosterSearchController.searchRosterExperts(id)
GET           /api/search/roster/:id/experts/agg                                                                         controllers.search.RosterSearchController.searchRosterExpertsAgg(id)
GET           /api/search/roster/:id/experts/advanced                                                                    controllers.search.RosterSearchController.searchRosterExpertsAdvc(id)
GET           /api/search/roster/:id/experts/advanced/agg                                                                controllers.search.RosterSearchController.searchRosterExpertsAdvcAgg(id)

GET           /api/search/entity/:query                                                                                  controllers.search.SearchController.getEntity(query)

# for xuetangx.com
GET           /api/xt/search/entity/:query                                                                               controllers.search.SearchController.getEntity4XueTang(query)

#for abbreviation
GET           /api/abbreviation/:query                                                                                   controllers.abbreviation.AbbreviationController.getPhrase(query)
POST          /api/abbreviation/mappings                                                                                 controllers.abbreviation.CrossLanguageMappingController.getMappings
PUT           /api/abbreviation/mappings                                                                                 controllers.abbreviation.CrossLanguageMappingController.setMappings
GET           /api/abbreviation/mapping/:query                                                                           controllers.abbreviation.CrossLanguageMappingController.getMapping(query)

# Person
GET           /api/person/:id                                                                                            controllers.person.PersonController.getPersonById(id)
GET           /api/person/summary/:id                                                                                    controllers.person.PersonController.getPersonSummaryById(id)
GET           /api/person/infocard/:id                                                                                   controllers.person.PersonController.getPersonInfoCardById(id)
POST          /api/person/batch-list                                                                                     controllers.person.PersonController.getPersonsByIds

GET           /api/person/activity/:id/indices                                                                           controllers.activity.ActivityScoreController.getActivityCompreScoresByPersonId(id)

GET           /api/person/pubs/:id/info                                                                                  controllers.person.PersonController.getPersonPubBrowseMap(id)

GET           /api/person/pubs/:id/stats                                                                                 controllers.person.PersonController.getPersonPubsStats(id)
GET           /api/person/patents/:id/stats                                                                              controllers.person.PersonController.getPersonPatentsStats(id)
#TODO deprecated start
#GET           /api/person/pubs/:id/po/all/size/:size/page/:page          controllers.person.PersonController.getPersonPopularPubListByIdOffsetCount(id,size:Int,page:Int)
#GET           /api/person/pubs/:id/po/nc/lo/:nc_lo/hi/:nc_hi             controllers.person.PersonController.getPersonPopularPubListByIdNCites(id,nc_lo:Int,nc_hi:Int)
#GET           /api/person/pubs/:id/size/:size/page/:page/year/:year      controllers.person.PersonController.getPersonPubListById(id,size:Int,page:Int,year:Int)
#TODO deprecated end


GET           /api/person/pubs/:id/all/year/:offset/:size                                                                controllers.person.PersonController.getRecentPublist(id,offset:Int,size:Int)
GET           /api/person/pubs/:id/all/citation/:offset/:size                                                            controllers.person.PersonController.getPopularPublist(id,offset:Int,size:Int)
GET           /api/person/pubs/:id/range/citation/:nc_lo/:nc_hi/:offset/:size                                            controllers.person.PersonController.getPopularPublistInCitationRange(id,nc_lo:Int,nc_hi:Int,offset:Int,size:Int)
GET           /api/person/pubs/:id/range/year/:year/:offset/:size                                                        controllers.person.PersonController.getRecentPublistInYearRange(id, year:Int, offset:Int, size: Int)

GET           /api/person/pubs/:id/tobeconfirmed/:offset/:size                                                           controllers.person.PersonController.getToBeConfirmedPubs(id, offset:Int, size: Int)
POST          /api/person/pubs/:aid/confirm/:pid                                                                         controllers.person.PersonController.confirmPubs(aid, pid)
GET           /api/person/pubs/:aid/confirm/size                                                                         controllers.person.PersonController.getToBeConfirmedPubSize(aid: String)

GET           /api/person/patents/:id/all/year/:offset/:size                                                             controllers.person.PersonController.getRecentPatentList(id,offset:Int,size:Int)
GET           /api/person/patents/:id/range/year/:year/:offset/:size                                                     controllers.person.PersonController.getRecentPatentlistInYearRange(id, year:Int, offset:Int, size: Int)
GET           /api/person/projects/:id/all/year/:offset/:size                                                            controllers.person.PersonController.getRecentProjectList(id,offset:Int,size:Int)


GET           /api/person/indices/:id                                                                                    controllers.person.PersonController.getPersonIndicesById(id)
GET           /api/person/indices/dcore/:aids                                                                            controllers.person.DCoreIndicesController.getDCoreIndicesByAid(aids)
GET           /api/person/interests/:id                                                                                  controllers.person.PersonController.getPersonInterestsById(id)
GET           /api/person/lectures/:id                                                                                   controllers.person.PersonController.getVideoLecturesById(id)
GET           /api/person/email/i/:id                                                                                    controllers.person.PersonController.getEmailImage(id)
GET           /api/person/email/s/:id                                                                                    controllers.person.PersonController.getEmailString(id)
GET           /api/person/email-cr/i/:id                                                                                 controllers.person.PersonController.getEmailCrImage(id)
GET           /api/person/email-cr/s/:id                                                                                 controllers.person.PersonController.getEmailCrString(id)
#GET           /api/person/lecture_thumb/:id                                controllers.person.PersonController.getVideoLectureThumbById(id)

GET           /api/person/similar/:id                                                                                    controllers.person.PersonController.getSimilarPersonsInfoById(id)

GET           /api/person/from-old-id/:oid                                                                               controllers.person.PersonController.getPersonIdByOid(oid:Int)
GET           /api/person/from-nsfc-id/:nsfcid                                                                           controllers.person.PersonController.getPersonIdByNsfcId(nsfcid:Int)

POST          /api/person/avatar/update/link                                                                             controllers.person.PersonController.updateAvatarByOutsideLink
POST          /api/person/avatar/update/file                                                                             controllers.person.PersonController.updateAvatarByFile
POST          /api/person/avatar/list                                                                                    controllers.person.PersonController.getPersonAvatarsByIds


GET           /api/person/ego/:id                                                                                        controllers.person.PersonController.getPersonEgoNetById(id: String)
GET           /api/person/ca/:id/:offset/:size                                                                           controllers.person.PersonController.getPersonCoauthorsInfoById(id: String, offset: Int, size: Int)
POST          /api/person/refresh/:id                                                                                    controllers.person.PersonController.refreshIds(id: String)

GET           /api/person/award-tags/:id/offset/:offset/size/:size                                                       controllers.person.PersonController.listAwardsByAid(id: String, offset: Int, size: Int)

POST          /api/person/contact/modify                                                                                 controllers.person.PersonController.contactModify
POST          /api/person/rel/modify                                                                                     controllers.person.PersonController.relationModify


POST          /api/person/exp/work/:id                                                                                   controllers.aff.ExperienceController.addNewWorkExperience(id)
PUT           /api/person/exp/work/:id/weid/:weid                                                                        controllers.aff.ExperienceController.updateWorkExperience(id, weid)
DELETE        /api/person/exp/work/:id/all                                                                               controllers.aff.ExperienceController.clearWorkExperience(id)
DELETE        /api/person/exp/work/:id/weid/:weid                                                                        controllers.aff.ExperienceController.deleteWorkExperience(id, weid)


# Is Me / Not Me
GET           /api/person/isbind/:id                                                                                     controllers.person.PersonController.checkPersonIsBinded(id)
GET           /api/person/pos_check/:aid/:pid                                                                            controllers.person.PersonController.checkPosByAidNdPid(aid,pid)

#TODO update
POST          /api/person/bind                                                                                           controllers.person.PersonController.addPubToPerson
POST          /api/person/unbind                                                                                         controllers.person.PersonController.removePubFromPerson

POST          /api/person/pubs                                                                                           controllers.person.PersonController.addPubsToPerson
DELETE        /api/person/pubs                                                                                           controllers.person.PersonController.removePubsFromPerson

#GEO
PUT           /api/person/geo/:id                                                                                        controllers.person.PersonGeoController.updatePersonGeo(id)


# Affiliation
GET           /api/aff/paid/:paid/offset/:offset/size/:size                                                              controllers.aff.AffiliationController.listAffsByParentId(paid, offset:Int, size:Int)

GET           /api/aff/summary/:id                                                                                       controllers.aff.AffiliationController.getAffSummaryById(id)
GET           /api/aff/iid/:iid/members/offset/:offset/size/:size                                                        controllers.aff.ExperienceController.listExpertsWithInstId(iid, offset:Int, size:Int)
GET           /api/aff/iid/:iid/members/agg                                                                              controllers.aff.ExperienceController.listExpertsWithInstIdAgg(iid)

PUT           /api/aff/info/:id                                                                                          controllers.aff.AffiliationController.updateInfoOfAffById(id)
PUT           /api/aff/logo/:id                                                                                          controllers.aff.AffiliationController.uploadLogoOfAffById(id)
PUT           /api/aff/bg/:id                                                                                            controllers.aff.AffiliationController.uploadBackgroundOfAffById(id)

POST          /api/aff                                                                                                   controllers.aff.AffiliationController.addAff()

PUT           /api/aff/label/removed/:id                                                                                 controllers.aff.AffiliationController.labelAffAsRemoved(id)
DELETE        /api/aff/label/removed/:id                                                                                 controllers.aff.AffiliationController.labelAffAsUnRemoved(id)

GET           /api/aff/pubs/agg/:iid                                                                                     controllers.aff.AffiliationPubsController.getPubAggsByIid(iid)
GET           /api/aff/pubs/iid/:iid/all/offset/:offset/size/:size                                                       controllers.aff.AffiliationPubsController.listAllRecentPubsByIid(iid,offset:Int,size:Int)
GET           /api/aff/pubs/iid/:iid/all/year/offset/:offset/size/:size                                                  controllers.aff.AffiliationPubsController.listAllRecentPubsByIid(iid,offset:Int,size:Int)
GET           /api/aff/pubs/iid/:iid/all/cite/offset/:offset/size/:size                                                  controllers.aff.AffiliationPubsController.listTopCitedPubsByIid(iid,offset:Int,size:Int)
GET           /api/aff/pubs/iid/:iid/year/:year/offset/:offset/size/:size                                                controllers.aff.AffiliationPubsController.listPubsByYear(iid,year:Int, offset:Int,size:Int)
GET           /api/aff/pubs/iid/:iid/cite/:cil/:cih/offset/:offset/size/:size                                            controllers.aff.AffiliationPubsController.listPubsByNCite(iid,cil:Long,cih:Long,offset:Int,size:Int)

GET           /api/aff/pubs/tag/:tag/agg/:iid                                                                            controllers.aff.AffiliationPubsController.getPubAggsByIidWithTag(iid,tag)
GET           /api/aff/pubs/tag/:tag/iid/:iid/all/offset/:offset/size/:size                                              controllers.aff.AffiliationPubsController.listAllRecentPubsByIidWithTag(iid,tag,offset:Int,size:Int)
GET           /api/aff/pubs/tag/:tag/iid/:iid/year/:year/offset/:offset/size/:size                                       controllers.aff.AffiliationPubsController.listPubsByYearWithTag(iid,tag,year:Int, offset:Int,size:Int)
POST          /api/aff/pubs/:iid/update                                                                                  controllers.aff.AffiliationPubsController.updatePubs(iid)
POST          /api/aff/pubs/tag/:tag/:iid/update                                                                         controllers.aff.AffiliationPubsController.updatePubsWithTag(iid, tag: String)
POST          /api/aff/pubs/tag/:tag/:iid/clear                                                                          controllers.aff.AffiliationPubsController.clearPubsWithTag(iid, tag: String)
POST          /api/aff/pubs/:iid/clear                                                                                   controllers.aff.AffiliationPubsController.clearPubs(iid)
POST          /api/aff/esipubstag/clear                                                                                  controllers.aff.AffiliationPubsController.removePubESITag




GET           /api/aff/pubs/featured                                                                                     controllers.aff.AffiliationPubsController.listFeaturedPubsInAff()

# TODO add person to inst, for the requirement of sz
# POST          /api/aff/add-person/iid/:iid                                                                               controllers.aff.AffiliationPubsController.listFeaturedPubsInAff()


GET           /api/aff/patents/agg/:iid                                                                                  controllers.aff.AffiliationPatentsController.getPatentAggsByIid(iid)
GET           /api/aff/patents/iid/:iid/all/offset/:offset/size/:size                                                    controllers.aff.AffiliationPatentsController.listAllRecentPatentsByIid(iid,offset:Int,size:Int)
GET           /api/aff/patents/iid/:iid/year/:year/offset/:offset/size/:size                                             controllers.aff.AffiliationPatentsController.listPatentsByYear(iid, year:Int, offset:Int,size:Int)
POST          /api/aff/patents/:iid/update                                                                               controllers.aff.AffiliationPatentsController.updatePatents(iid)
POST          /api/aff/patents/:iid/clear                                                                                controllers.aff.AffiliationPatentsController.clearPatents(iid)

GET           /api/aff/projects/agg/:iid                                                                                 controllers.aff.AffiliationProjectController.getProjectAggsByIid(iid)
GET           /api/aff/projects/iid/:iid/all/offset/:offset/size/:size                                                   controllers.aff.AffiliationProjectController.listAllRecentProjectsByIid(iid,offset:Int,size:Int)
GET           /api/aff/projects/iid/:iid/year/:year/offset/:offset/size/:size                                            controllers.aff.AffiliationProjectController.listProjectsByYear(iid,year:Int, offset:Int,size:Int)
POST          /api/aff/projects/:iid/update                                                                              controllers.aff.AffiliationProjectController.updateProjects(iid)
POST          /api/aff/projects/:iid/clear                                                                               controllers.aff.AffiliationProjectController.clearProjects(iid)

GET           /api/aff/stats/all/:iid                                                                                    controllers.aff.InstitutionStatsController.getGeneralInformation(iid)
POST          /api/aff/stats/merged                                                                                      controllers.aff.InstitutionStatsController.getMergedInstStats()
GET           /api/social/linkedin/:id                                                                                   controllers.social.SocialIntegrationController.getLinkedinProfile(id)

# Protected
POST          /api/aff/person/protected/:iid                                                                             controllers.aff.InstitutionMembersManageController.addInstAsProtectedByIid(iid)
DELETE        /api/aff/person/protected/:iid                                                                             controllers.aff.InstitutionMembersManageController.rmInstFromProtectedByIid(iid)
PUT           /api/aff/person/protected/:iid                                                                             controllers.aff.InstitutionMembersManageController.syncProtectedInstByIid(iid)

POST          /api/aff/person/protected/:iid/staff/sync                                                                  controllers.aff.InstitutionMembersManageController.addAllExpertsToProtectedInst(iid)
DELETE        /api/aff/person/protected/:iid/staff/sync                                                                  controllers.aff.InstitutionMembersManageController.clearExpertsFromProtectedInst(iid)

# Publication
GET           /api/pub/:id                                                                                               controllers.pub.PublicationController.getPubById(id)
GET           /api/pub/summary/doi/:dpx/:dsx                                                                             controllers.pub.PublicationController.getPubSummaryByDOI(dpx, dsx)
GET           /api/pub/summary/:id                                                                                       controllers.pub.PublicationController.getPubSummaryById(id)
GET           /api/pub/abstract/:id                                                                                      controllers.pub.PublicationController.getPubAbstractById(id)

GET           /api/pub/bib/:id                                                                                           controllers.pub.PublicationController.getBiBTeXByPid(id)
GET           /api/pub/ctext/:id                                                                                         controllers.pub.PublicationController.getCiteTextByPid(id)
# GET           /api/pub/venueid/:id/:yearlo/:yearhi                        controllers.pub.PublicationController.getPubsByVDid(id,yearlo:Int,yearhi:Int)
GET           /api/pub/venueid/:id/:yearlo/:yearhi                                                                       controllers.pub.PublicationController.getPubsByVfid(id,yearlo:Int,yearhi:Int)
GET           /api/pub/venueid/:id/:yearlo/:yearhi/:offset/:limit                                                        controllers.pub.PublicationController.getPubsByVfidTopCited(id,yearlo:Int,yearhi:Int,offset:Int,limit:Int)

# pdf for publication , TODO: rewrite
POST          /api/pub/pdf/upload                                                                                        controllers.bifrost.PublicationUploadController.uploadPDF
POST          /api/pub/pdf/uploadSimple                                                                                  controllers.bifrost.PublicationUploadController.uploadPDFSimple
POST          /api/pub/pdf/confirm                                                                                       controllers.bifrost.PublicationUploadController.updateMeta

POST          /api/pub/create/meta                                                                                       controllers.bifrost.PublicationUploadController.createNewPubFromMeta
POST          /api/pub/create/file                                                                                       controllers.bifrost.PublicationUploadController.createNewPubFromFile
POST          /api/pub/create/esi/file                                                                                   controllers.bifrost.PublicationUploadController.createEsiPubFromFile
GET           /api/pub/export/batch/:aid/offset/:offset/size/:size                                                       controllers.pub.PublicationController.pubExport(aid,offset:Int,size:Int)
GET           /api/pub/export/batch/:aid/offset/:offset/size/:size/data.csv                                              controllers.pub.PublicationController.pubExport(aid,offset:Int,size:Int)

GET           /api/pub/isbind/:id/:pos                                                                                   controllers.person.PersonController.checkPubIsBinded(id,pos:Int)

POST          /api/pub/ncitation                                                                                         controllers.bifrost.PublicationBifrostController.ncitationUpdate
POST          /api/pub/ncitation/batch                                                                                   controllers.bifrost.PublicationBifrostController.ncitationBatchUpdate

POST          /api/pub/rating/save/:pid                                                                                  controllers.pub.PublicationController.saveRating(pid)
GET           /api/pub/rating/get/:pid                                                                                   controllers.pub.PublicationController.getRating(pid)
GET           /api/pub/rating/getu/:pid                                                                                  controllers.pub.PublicationController.getUserRating(pid)


GET           /api/pub/cite/:id/rec/offset/:offset/size/:size                                                            controllers.pub.PublicationCitationController.recentCitesByPid(id, offset:Int, size:Int)
GET           /api/pub/ref/:id/offset/:offset/size/:size                                                                 controllers.pub.PublicationCitationController.refsByPid(id, offset:Int, size:Int)

# Similar Pubs
GET           /api/pub/sim/:id/offset/:offset/size/:size                                                                 controllers.pub.SimPublicationController.similarPubsByPid(id, offset:Int, size:Int)

# Tags In Pub
GET           /api/pub/tag/pid/:pid/g/:op/offset/:offset/size/:size                                                      controllers.pub.PublicationTagsController.listGlobalTagsForPub(op, pid, offset:Int, size:Int)
GET           /api/pub/tag/pid/:pid/u/:op/offset/:offset/size/:size                                                      controllers.pub.PublicationTagsController.listUserTagsForPub(op, pid, offset:Int, size:Int)
GET           /api/pub/tag/pid/:pid/voters/:op/offset/:offset/size/:size/mt/:mt                                          controllers.pub.PublicationTagsController.pubTopicVoterByMention(op, pid, mt, offset:Int, size:Int)
GET           /api/pub/tag/pid/:pid/voters/:op/offset/:offset/size/:size/tid/:tid                                        controllers.pub.PublicationTagsController.pubTopicVoterByTopicId(op, pid, tid, offset:Int, size:Int)
GET           /api/pub/tag/user/:op/offset/:offset/size/:size                                                            controllers.pub.PublicationTagsController.listAllUserTags(op, offset:Int, size:Int)
GET           /api/pub/tag/user/:op/offset/:offset/size/:size/tid/:tid/pubs                                              controllers.pub.PublicationTagsController.listVotedPubByUidAndTid(op, tid, offset:Int, size:Int)

POST          /api/pub/tag/pid/:pid/u/:op/tag/:tag                                                                       controllers.pub.PublicationTagsController.addTagToPub(op, pid, tag)
DELETE        /api/pub/tag/pid/:pid/u/:op/tag/:tag                                                                       controllers.pub.PublicationTagsController.removeTagFromPub(op, pid, tag)

POST          /api/pub/user-pending/batch                                                                                controllers.pub.UserPendingPublicationController.batchCreateUserPendingPub
DELETE        /api/pub/user-pending/batch                                                                                controllers.pub.UserPendingPublicationController.batchDiscardUserPedingPub
POST          /api/pub/user-pending/batch/submit                                                                         controllers.pub.UserPendingPublicationController.batchSubmitUserPedingPub

POST          /api/pub/user-pending                                                                                      controllers.pub.UserPendingPublicationController.createUserPendingPub
GET           /api/pub/user-pending/offset/:offset/size/:size                                                            controllers.pub.UserPendingPublicationController.listUserPendingPubs(offset: Int, size: Int)
GET           /api/pub/user-pending/:id                                                                                  controllers.pub.UserPendingPublicationController.getUserPendingPub(id)
DELETE        /api/pub/user-pending/:id                                                                                  controllers.pub.UserPendingPublicationController.discardUserPedingPub(id)
PATCH         /api/pub/user-pending/:id                                                                                  controllers.pub.UserPendingPublicationController.gatherInfoInUserPending(id)
DELETE        /api/pub/user-pending/:id/dupl                                                                             controllers.pub.UserPendingPublicationController.notDuplInUserPending(id)
POST          /api/pub/user-pending/:id/submit                                                                           controllers.pub.UserPendingPublicationController.submitUserPedingPub(id)
PUT           /api/pub/user-pending/:id/users                                                                            controllers.pub.UserPendingPublicationController.modifyAuthorList(id)

# Track
DELETE        /api/track/pub/:pid                                                                                        controllers.track.PubTrackController.delUser2PubTrackEvent(pid)
GET           /api/track/pub/offset/:offset/size/:size                                                                   controllers.track.PubTrackController.listUser2PubTrackEvents(offset:Int, size:Int)
DELETE        /api/track/pub/recent/:scale                                                                               controllers.track.PubTrackController.cleanRecentUser2PubTrackEvents(scale)

DELETE        /api/track/person/:aid                                                                                     controllers.track.PersonTrackController.delUser2PersonTrackEvent(aid)
GET           /api/track/person/offset/:offset/size/:size                                                                controllers.track.PersonTrackController.listUser2PersonTrackEvents(offset:Int, size:Int)
DELETE        /api/track/person/recent/:scale                                                                            controllers.track.PersonTrackController.cleanRecentUser2PersonTrackEvents(scale)

GET           /api/track/person/rec/:num                                                                                 controllers.track.PersonTrackController.personTrendingRec(num:Int)

DELETE        /api/track/query/:qid                                                                                      controllers.track.QueryTrackController.delUser2QueryTrackEvent(qid)
GET           /api/track/query/offset/:offset/size/:size                                                                 controllers.track.QueryTrackController.listUser2QueryTrackEvents(offset:Int, size:Int)
DELETE        /api/track/query/recent/:scale                                                                             controllers.track.QueryTrackController.cleanRecentUser2QueryTrackEvents(scale)


# Patent
GET           /api/patent/:name/:start/:size                                                                             controllers.patent.PatentController.getPatentsByName(name, start: Int, size: Int)
GET           /api/patent/get/:id                                                                                        controllers.patent.PatentController.getPatentById(id)
POST          /api/patent/upload/meta                                                                                    controllers.patent.PatentController.uploadNewPatentFromMeta
POST          /api/patent/upload/file                                                                                    controllers.patent.PatentController.uploadNewPatentFromFile
DELETE        /api/person/patents                                                                                        controllers.person.PersonController.removePatentsFromPerson

# Ranks
GET           /api/rank/person/overall                                                                                   controllers.rank.RankController.getRankPersonOverall
GET           /api/rank/person/:attr/:offset/:size                                                                       controllers.rank.RankController.getRankPerson(attr, offset: Int, size: Int)
GET           /api/rank/org/meta                                                                                         controllers.rank.RankController.getOrgRankMeta
GET           /api/rank/org/list/:domain/:_type/:rank/:start/:length                                                     controllers.rank.RankController.getOrgRanks(domain: Int, _type:  Int,  rank: String, start: Int, length: Int)
GET           /api/rank/org/search/:domain/:_type/:rank/:idorg/:length                                                   controllers.rank.RankController.searchOrgRankById(domain: Int, _type: Int, rank: String, idorg: Int, length: Int)

GET           /api/rank/conf/list/:_type                                                                                 controllers.rank.RankController.getVenueFusionRanksByH5Index(_type:Int)
GET           /api/rank/conf/ifa/:_type                                                                                  controllers.rank.RankController.getVenueFusionRanksByH5Index(_type:Int)

GET           /api/rank/conf/cs/h5/:area                                                                                 controllers.rank.VenueRankController.listCachedVenueChainByCSArea(area:Int)

#TODO remove start
GET           /api/rank/bestpapers                                                                                       controllers.rank.RankController.getBestPapers
GET           /api/rank/bestpapers/refresh                                                                               controllers.rank.RankController.refreshBestPapers
#TODO remove end


GET           /api/rank/bestpapers/allvenue                                                                              controllers.rank.BestPaperController.getBestPaperOverview
GET           /api/rank/bestpapers/:vid                                                                                  controllers.rank.BestPaperController.listTopAndBestPapersByVid(vid: String)

# LeaderBoard
GET           /api/leaderboard/person/overall                                                                            controllers.rank.PersonLeaderBoardController.topRankedOverview
GET           /api/leaderboard/person/list/:attr/offset/:offset/size/:size                                               controllers.rank.PersonLeaderBoardController.listTopRankedPersons(attr, offset:Int, size:Int)

POST          /api/leaderboard/person/i/:id/reject                                                                       controllers.rank.PersonLeaderBoardController.doRejectOnePerson(id)
DELETE        /api/leaderboard/person/i/:id/reject                                                                       controllers.rank.PersonLeaderBoardController.undoRejectOnePerson(id)


# Venue
# TODO removed start
GET           /api/venue/:id                                                                                             controllers.venue.VenueController.getVenueFusionById(id)
GET           /api/venue/cid/:cid                                                                                        controllers.venue.VenueController.getVenueFusionByCid(cid)
# TODO removed end
GET           /api/venue/summary/:id                                                                                     controllers.venue.VenueController.getVenueChainbyId(id)
GET           /api/venue/hint/:qs                                                                                        controllers.venue.VenueController.getVenueHint(qs)
GET           /api/venue/stats/all/:vid/:yearl/:yearh                                                                    controllers.venue.VenueStatsController.getAllInfo(vid, yearl:Int, yearh:Int)
GET           /api/venue/contextour/:id/:type                                                                            controllers.venue.VenueController.getContextour(id, type:Int)


POST          /api/venue/analysis/jtat                                                                                   controllers.venue.JournalTrendingAnalysisTaskController.createJTATask
GET           /api/venue/analysis/jtat/offset/:offset/size/:size                                                         controllers.venue.JournalTrendingAnalysisTaskController.listJTATasks(offset:Int, size:Int)
GET           /api/venue/analysis/jtat/:id                                                                               controllers.venue.JournalTrendingAnalysisTaskController.getJTATaskById(id)
PUT           /api/venue/analysis/jtat/:id                                                                               controllers.venue.JournalTrendingAnalysisTaskController.updateJTATask(id)
DELETE        /api/venue/analysis/jtat/:id                                                                               controllers.venue.JournalTrendingAnalysisTaskController.deleteJTATask(id)
GET           /api/venue/analysis/jtat/sample/journal/:vid/year/:year                                                    controllers.venue.JournalTrendingAnalysisTaskController.venueGetSampleWithYear(vid, year:Int)
GET           /api/venue/analysis/jtat/sample/journal/:vid                                                               controllers.venue.JournalTrendingAnalysisTaskController.venueGetSample(vid)

#Conference

#TODO all redesign
GET           /api/conference/paper/:query/:fromyear/:toyear/:startOffset                                                controllers.venue.ConferenceController.getPaperRank(query,fromyear:Int,toyear:Int,startOffset)
#GET         /api/conference/paper/:query                                         controllers.venue.ConferenceController.getPaperRank(query)
GET           /api/conference/author/:query/:fromyear/:toyear                                                            controllers.venue.ConferenceController.getAuthorRank(query,fromyear:Int,toyear:Int)
#GET         /api/conference/author/:query                                        controllers.venue.ConferenceController.getAuthorRank(query)
GET           /api/conference/distribution/:query/:fromyear/:toyear                                                      controllers.venue.ConferenceController.getDistribution(query,fromyear:Int,toyear:Int)
#GET         /api/conference/distribution/:query                                  controllers.venue.ConferenceController.getDistribution(query)
GET           /api/conference/keywords/:query                                                                            controllers.venue.ConferenceController.getKeywords(query)
GET           /api/conference/allinfo/:query/:fromyear/:toyear                                                           controllers.venue.ConferenceController.getAllInfo(query,fromyear:Int,toyear:Int)

# ImportantUserLog
POST          /api/event/person/sim                                                                                      controllers.event.SimPersonEventController.simPersonEvent
POST          /api/event/person/follow                                                                                   controllers.event.SimPersonEventController.followExpertEvent
POST          /api/event/person/mark                                                                                     controllers.event.SimPersonEventController.markPubEvent
POST          /api/event/person/activity                                                                                 controllers.event.SimPersonEventController.activityClickEvent
POST          /api/event/person/event                                                                                    controllers.event.SimPersonEventController.addUserEvent

# Activity
GET           /api/activity/all                                                                                          controllers.activity.ActivityController.getAllActivities
GET           /api/activity/list/offset/:offset/size/:size                                                               controllers.activity.ActivityController.listActivities(offset:Int,size:Int)
GET           /api/activity/sys/offset/:offset/size/:size                                                                controllers.activity.ActivityController.listActivitiesBySys(offset:Int,size:Int)
GET           /api/activity/upcoming                                                                                     controllers.activity.ActivityController.getUpcomingActivities
GET           /api/activity/recom/user/:uid                                                                              controllers.activity.ActivityController.getRecommendedActivities(uid)
GET           /api/activity/:id                                                                                          controllers.activity.ActivityController.getActivityById(id)
POST          /api/activity/update                                                                                       controllers.activity.ActivityController.updateActivity
POST          /api/activity/update/admin                                                                                 controllers.activity.ActivityController.updateActivityByAdmin
POST          /api/activity/delete/:id                                                                                   controllers.activity.ActivityController.deleteActivityById(id)
POST          /api/activity/post_activity                                                                                controllers.activity.ActivityController.postActivity

POST          /api/activity/avatar                                                                                       controllers.activity.ActivityController.uploadAvatar
POST          /api/activity/img                                                                                          controllers.activity.ActivityController.uploadImg

GET           /api/activity/tags/:src/:num                                                                               controllers.activity.ActivityController.getTopMentionedTags(src, num:Int)

POST          /api/activity/ignore/:id                                                                                   controllers.activity.ActivityCommentController.ignoreActivity(id)
POST          /api/activity/like/:id                                                                                     controllers.activity.ActivityCommentController.like(id)
DELETE        /api/activity/like/:id                                                                                     controllers.activity.ActivityCommentController.unlike(id)


POST          /api/activity/tag/aid/:aid/u/:op/tag/:tag                                                                  controllers.activity.ActivityTagsController.addTagToActivity(op, aid, tag)
DELETE        /api/activity/tag/aid/:aid/u/:op/tag/:tag                                                                  controllers.activity.ActivityTagsController.removeTagFromActivity(op, aid, tag)

GET           /api/activity/tag/aid/:aid/g/:op/offset/:offset/size/:size                                                 controllers.activity.ActivityTagsController.listGlobalTagsForActivity(op, aid, offset:Int, size:Int)
GET           /api/activity/tag/aid/:aid/u/:op/offset/:offset/size/:size                                                 controllers.activity.ActivityTagsController.listUserTagsForActivity(op, aid, offset:Int, size:Int)

GET           /api/topic/activity/voted/topic/rank/:oper/mention/:mention/offset/:offset/size/:size                      controllers.activity.ActivityTagsController.topVotedActivityByMention(oper,mention,offset:Int,size:Int)
GET           /api/topic/activity/voted/topic/rank/:oper/id/:tid/offset/:offset/size/:size                               controllers.activity.ActivityTagsController.topVotedAcitvityByTopicId(oper,tid,offset:Int,size:Int)
GET           /api/activity/tag/user/:op/offset/:offset/size/:size                                                       controllers.activity.ActivityTagsController.listAllUserTags(op, offset:Int, size:Int)
GET           /api/activity/tag/user/:op/offset/:offset/size/:size/tid/:tid                                              controllers.activity.ActivityTagsController.listVotedActByUidAndTid(op, tid, offset:Int, size:Int)

POST          /api/activity/massive                                                                                      controllers.activity.ActivityController.postMassiveActivities

POST          /api/activity/speaker/suggest                                                                              controllers.activity.ActivityController.speakerSuggest

POST          /api/activity/score/me/:src/:actid/:aid/:key/:score/:lvtime                                                controllers.activity.ActivityScoreController.updateOrSaveActivityScore(src, actid, aid, key, score: Double, lvtime: Long)
DELETE        /api/activity/score/me/:src/:actid/:aid/:key                                                               controllers.activity.ActivityScoreController.rmActivityScore(src, actid, aid, key)

GET           /api/activity/score/:uid/:src/:actid/:aid/:key                                                             controllers.activity.ActivityScoreController.getActivityScore(uid, src, actid, aid, key)
GET           /api/activity/score-list/:uid/:src/:actid                                                                  controllers.activity.ActivityScoreController.listActivityScores(uid, src, actid)
GET           /api/activity/score-stats/:uid/:src/:actid/:aid/:tsl/:tsh                                                  controllers.activity.ActivityScoreController.statActivityScores(uid, src, actid, aid, tsl: Long, tsh: Long)

GET           /api/activity/admin/stats                                                                                  controllers.activity.ActivityScoreController.getStatsOfCcfActivities

#Wechat
GET           /api/wechat                                                                                                controllers.wechat.WechatController.validation(signature: String, timestamp: String, nonce: String, echostr: String)
POST          /api/wechat                                                                                                controllers.wechat.WechatController.serviceEntrance(signature: String, timestamp: String, nonce: String)
GET           /api/wechat/activity/:aid                                                                                  controllers.wechat.WechatController.viewActivity(aid: String, code: String, state: String)

# CAE
GET           /api/cae/conf/all                                                                                          controllers.cae.CAEController.getAllConfs
GET           /api/cae/conf/filter/type/:ftype/id/:id/order/:order/rev/:rev                                              controllers.cae.CAEController.getFiltertedConfs(ftype, id , order, rev: Int)
GET           /api/cae/conf/type                                                                                         controllers.cae.CAEController.getTypeMap
GET           /api/cae/conf/stats                                                                                        controllers.cae.CAEController.getConfStats
GET           /api/cae/conf/stats/location                                                                               controllers.cae.CAEController.getConfLocationStats

GET           /api/cae/conf/:cid                                                                                         controllers.cae.CAEController.getConf(cid:Long)
GET           /api/cae/conf/expert/:cid                                                                                  controllers.cae.CAEController.getExpertsByCid(cid:Long)
GET           /api/cae/conf/achievement/:cid                                                                             controllers.cae.CAEController.getAchsByCid(cid:Long)

GET           /api/cae/conf/geo/overview                                                                                 controllers.cae.CAEController.getConfLocationStats
GET           /api/cae/conf/geo/experts/loc/:loc/offset/:offset/size/:size                                               controllers.cae.CAEController.listExpertsByLocation(loc,offset:Int,size:Int)
GET           /api/cae/conf/geo/confs/loc/:loc/offset/:offset/size/:size                                                 controllers.cae.CAEController.listConfsByLocation(loc,offset:Int,size:Int)
GET           /api/cae/conf/geo/locations/eid/:eid/offset/:offset/size/:size                                             controllers.cae.CAEController.listLocationByExpertId(eid:Long,offset:Int,size:Int)


PUT           /api/cae/conf/eid/:eid/auid/:auid                                                                          controllers.cae.CAEController.setAuidToExpert(eid:Long, auid:String)

GET           /api/cae/tag/cloud/draft/offset/:offset/size/:size                                                         controllers.cae.CAEController.getTagCloudDraft(offset: Int, size: Int)
GET           /api/cae/tag/cloud/release/offset/:offset/size/:size                                                       controllers.cae.CAEController.getTagCloudRelease(offset: Int, size: Int)
POST          /api/cae/tag/cloud/modify/:tag                                                                             controllers.cae.CAEController.addTagAsModified(tag)
DELETE        /api/cae/tag/cloud/modify/:tag                                                                             controllers.cae.CAEController.removeTagFromModified(tag)

# CAE SEARCH
GET           /api/cae/search                                                                                            controllers.cae.CAEController.search


# Article
POST          /api/article                                                                                               controllers.article.ArticleController.addArticle
GET           /api/article/:id                                                                                           controllers.article.ArticleController.getArticleById(id)
DELETE        /api/article/:id                                                                                           controllers.article.ArticleController.removeArticleById(id)
GET           /api/article/alias/:alias                                                                                  controllers.article.ArticleController.getArticleByAlias(alias)
POST          /api/article/prop/:id                                                                                      controllers.article.ArticleController.updateArticleProps(id)
POST          /api/article/blk/:id                                                                                       controllers.article.ArticleController.updateArticleBlock(id)
GET           /api/article/list/:id/:offset/:size                                                                        controllers.article.ArticleController.getPageListByUid(id,offset:Int,size:Int)

# Article Attachment
POST          /api/article/attachment                                                                                    controllers.article.ArticleController.addAttachmentFile

# Roster
POST          /api/roster                                                                                                controllers.roster.RosterController.createRoster
POST          /api/roster/advc                                                                                           controllers.roster.RosterController.createAdvancedRoster
GET           /api/roster/offset/:offset/size/:size                                                                      controllers.roster.RosterController.listRosters(offset: Int, size: Int)
GET           /api/roster/list/:cag/offset/:offset/size/:size                                                            controllers.roster.RosterController.listRostersByCategories(offset: Int, size: Int, cag)
GET           /api/roster/note/:aid                                                                                      controllers.roster.RosterController.getNote(aid)
POST          /api/roster/note                                                                                           controllers.roster.RosterController.addNote()
GET           /api/roster/ac/:email/dl/:lymd/dh/:hymd/p/:offset/:size                                                    controllers.roster.RosterController.getAnnotatedProfilesByDate(email: String, lymd, hymd, offset: Int, size: Int)

DELETE        /api/roster/:id                                                                                            controllers.roster.RosterController.destroyRoster(id)
GET           /api/roster/:id                                                                                            controllers.roster.RosterController.getRosterById(id)
GET           /api/roster/alias/:alias                                                                                   controllers.roster.RosterController.getRosterByAlias(alias)
GET           /api/roster/mix/:mix                                                                                       controllers.roster.RosterController.getRosterByIdOrAlias(mix)

PUT           /api/roster/:id                                                                                            controllers.roster.RosterController.updateRosterBasicInfo(id)

GET           /api/roster/:id/agg                                                                                        controllers.roster.RosterController.getRosterPersonsAggs(id)

GET           /api/roster/:id/offset/:offset/size/:size                                                                  controllers.roster.RosterController.listRosterPersons(id, offset: Int, size: Int)
GET           /api/roster/:id/order-by/:order/offset/:offset/size/:size                                                  controllers.roster.RosterController.listRosterPersonsInOrder(id, order, offset: Int, size: Int)



PUT           /api/roster/:id/a/:aid                                                                                     controllers.roster.RosterController.addRosterPerson(id,aid)
PUT           /api/roster/:id/a                                                                                          controllers.roster.RosterController.addRosterPersons(id)
PUT           /api/roster/:id/a/srctid/:srctid                                                                           controllers.roster.RosterController.addAllRosterPersons(id, srctid)

PUT           /api/roster/:id/a/:aid/attr                                                                                controllers.roster.RosterController.updateRosterPersonAttr(id,aid)



PUT           /api/roster/:id/u/n/:nid/o/:oid                                                                            controllers.roster.RosterController.updateRoster(id,nid,oid)

DELETE        /api/roster/:id/d/:oid                                                                                     controllers.roster.RosterController.rmRosterPerson(id,oid)
GET           /api/roster/:id/uas/:size                                                                                  controllers.roster.RosterController.listUnassignedPersons(id,size:Int)
DELETE        /api/roster/:id/pop                                                                                        controllers.roster.RosterController.rosterPopUnassignedPerson(id)
PUT           /api/roster/:id/delay                                                                                      controllers.roster.RosterController.delayUnassignedPerson(id)
POST          /api/roster/:id/blank                                                                                      controllers.roster.RosterController.createNewPersonFromPendingObjects(id)
GET           /api/roster/:id/members/:uoffset/:usize/:goffset/:gsize                                                    controllers.roster.RosterController.listRosterMembers(id,uoffset:Int,usize:Int,goffset:Int,gsize:Int)
GET           /api/roster/:id/members/perm                                                                               controllers.roster.RosterController.getRosterMemberPerms(id)
PUT           /api/roster/:id/members/u                                                                                  controllers.roster.RosterController.updateRosterMember(id)
DELETE        /api/roster/:id/members/u/:uid                                                                             controllers.roster.RosterController.rmRosterMember(id,uid)

POST          /api/roster/:id/refresh                                                                                    controllers.roster.RosterController.refreshRoster(id)

GET           /api/roster/:id/export/offset/:offset/size/:size                                                           controllers.roster.RosterController.rosterExport(id,offset:Int,size:Int)
GET           /api/roster/:id/export/offset/:offset/size/:size/data.csv                                                  controllers.roster.RosterController.rosterExport(id,offset:Int,size:Int)

GET           /api/roster/:id/export/s/offset/:offset/size/:size/:name                                                   controllers.roster.RosterController.rosterExportSimple(id,offset:Int,size:Int,name)
GET           /api/roster/:id/export/d/offset/:offset/size/:size/:name                                                   controllers.roster.RosterController.rosterExportDetail(id,offset:Int,size:Int,name)

POST          /api/roster/:id/crawl-task                                                                                 controllers.roster.RosterController.addCrawlTask(id)

POST          /api/roster/:id/nominate/eids                                                                              controllers.roster.RosterNominationController.doNominateMuti(id)
POST          /api/roster/:id/nominate/:aid                                                                              controllers.roster.RosterNominationController.doNominate(aid,id)
DELETE        /api/roster/:id/nominate/:aid                                                                              controllers.roster.RosterNominationController.undoNominate(aid,id)
GET           /api/roster/:id/nominate/aid/:aid/offset/:offset/size/:size                                                controllers.roster.RosterNominationController.recentNominator(aid,id,offset:Int,size:Int)
GET           /api/roster/:id/nominate/top/offset/:offset/size/:size/nsz/:nsz                                            controllers.roster.RosterNominationController.topNomineesByRid(id,offset:Int,size:Int, nsz:Int)

GET           /api/roster/:id/geo/offset/:offset/size/:size                                                              controllers.roster.RosterController.rosterExportGeo(id,offset:Int,size:Int)

GET           /api/roster/award/overview/offset/:offset/size/:size                                                       controllers.roster.AwardRosterController.listAwardRosters(offset: Int, size: Int)
GET           /api/roster/award/overview/beta/offset/:offset/size/:size                                                  controllers.roster.AwardRosterController.listAwardBetaRosters(offset: Int, size: Int)
GET           /api/roster/award/summary/:mix                                                                             controllers.roster.AwardRosterController.getAwardRosterByIdOrAlias(mix)
GET           /api/roster/award/:id/offset/:offset/size/:size                                                            controllers.roster.AwardRosterController.listAwardRosterPersons(id, offset: Int, size: Int)
GET           /api/roster/award/:id/order-by/:order/offset/:offset/size/:size                                            controllers.roster.AwardRosterController.listAwardRosterPersonsInOrder(id, order, offset: Int, size: Int)
GET           /api/roster/award/:id/agg                                                                                  controllers.roster.AwardRosterController.getAwardRosterPersonsAggs(id)
PUT           /api/roster/award/:id                                                                                      controllers.roster.AwardRosterController.updateAwardRosterBasicInfo(id)
POST          /api/roster/award/vote/:oper/:id/:aid                                                                      controllers.roster.AwardRosterController.doVote(oper,aid,id)
DELETE        /api/roster/award/vote/:id/:aid                                                                            controllers.roster.AwardRosterController.undoVote(aid,id)

GET           /api/roster/award/:alias/rank/:aid                                                                         controllers.roster.AwardRosterController.positionCheck(aid, alias)


GET           /api/roster/award/search/:id/experts                                                                       controllers.search.RosterSearchController.searchAwardRosterExperts(id)
GET           /api/roster/award/search/:id/experts/advc                                                                  controllers.search.RosterSearchController.searchAwardRosterExpertsAdvc(id)


# Topic

GET           /api/topic/summary/m/:mention                                                                              controllers.topic.TopicController.getTopicByMention(mention)
POST          /api/topic/summary/i/:id                                                                                   controllers.topic.TopicController.updateTopicInfo(id)

GET           /api/topic/freqs/m/list                                                                                    controllers.topic.TopicController.getFrequenciesByMentions

# Person In Topic
PUT           /api/topic/person/vote/:oper/:aid/mention/:mention                                                         controllers.topic.PersonTopicController.votePersonInSomeTopic(oper,aid,mention)

DELETE        /api/topic/person/vote/:aid/mention/:mention                                                               controllers.topic.PersonTopicController.unvotePersonInSomeTopic(aid,mention)
GET           /api/topic/person/vote/:oper/:aid/mention/:mention                                                         controllers.topic.PersonTopicController.numPersonVotedInTopic(oper,aid,mention)
GET           /api/topic/person/voter/:oper/:aid/mention/:mention/offset/:offset/size/:size                              controllers.topic.PersonTopicController.personTopicVoter(oper,aid,mention,offset:Int,size:Int)
GET           /api/topic/person/voted/topic/rank/:oper/mention/:mention/offset/:offset/size/:size                        controllers.topic.PersonTopicController.topVotedPersonByTopic(oper,mention,offset:Int,size:Int)
GET           /api/topic/person/voted/topic/rank/:oper/mention/:mention/offset/:offset/size/:size/voter/:maxVoter        controllers.topic.PersonTopicController.topVotedPersonWithVoterByTopic(oper,mention,offset:Int,size:Int,maxVoter:Int)
GET           /api/topic/topic/voted/person/rank/:oper/:aid/offset/:offset/size/:size                                    controllers.topic.PersonTopicController.topVotedTopicOfByPerson(oper,aid,offset:Int,size:Int)

PUT           /api/topic/person/vote/:oper/:aid/id/:tid                                                                  controllers.topic.PersonTopicController.votePersonInSomeTopicById(oper,aid,tid)

DELETE        /api/topic/person/vote/:aid/id/:tid                                                                        controllers.topic.PersonTopicController.unvotePersonInSomeTopicById(aid,tid)
GET           /api/topic/person/vote/:oper/:aid/id/:tid                                                                  controllers.topic.PersonTopicController.numPersonVotedInTopicById(oper,aid,tid)
GET           /api/topic/person/voter/:oper/:aid/id/:tid/offset/:offset/size/:size                                       controllers.topic.PersonTopicController.personTopicVoterById(oper,aid,tid,offset:Int,size:Int)
GET           /api/topic/person/voted/topic/rank/:oper/id/:tid/offset/:offset/size/:size                                 controllers.topic.PersonTopicController.topVotedPersonByTopicViaId(oper,tid,offset:Int,size:Int)
GET           /api/topic/person/voted/topic/rank/:oper/id/:tid/offset/:offset/size/:size/voter/:maxVoter                 controllers.topic.PersonTopicController.topVotedPersonWithVoterByTopicViaId(oper,tid,offset:Int,size:Int, maxVoter:Int)


GET           /api/topic/person/topics/:oper/:aid/toffset/:toffset/tsize/:tsize/uoffset/:uoffset/usize/:usize            controllers.topic.PersonTopicController.findVotedTopicsAndUsersByPersonId(oper,aid,toffset:Int,tsize:Int,uoffset:Int,usize:Int)

# Pubs In Topic

PUT           /api/topic/pub/vote/:oper/:aid/mention/:mention                                                            controllers.topic.PubTopicController.voteOnePubByMention(oper,aid,mention)

DELETE        /api/topic/pub/vote/:aid/mention/:mention                                                                  controllers.topic.PubTopicController.unvoteOnePubByMention(aid,mention)
GET           /api/topic/pub/vote/:oper/:aid/mention/:mention                                                            controllers.topic.PubTopicController.nUserVotedByMention(oper,aid,mention)
GET           /api/topic/pub/voter/:oper/:aid/mention/:mention/offset/:offset/size/:size                                 controllers.topic.PubTopicController.pubTopicVoterByMention(oper,aid,mention,offset:Int,size:Int)
GET           /api/topic/pub/voted/topic/rank/:oper/mention/:mention/offset/:offset/size/:size                           controllers.topic.PubTopicController.topVotedPubByMention(oper,mention,offset:Int,size:Int)
GET           /api/topic/pub/voted/topic/rank/:oper/mention/:mention/offset/:offset/size/:size/voter/:maxVoter           controllers.topic.PubTopicController.topVotedPubWithVoterByMention(oper,mention,offset:Int,size:Int,maxVoter:Int)
GET           /api/topic/topic/voted/person/rank/:oper/:aid/offset/:offset/size/:size                                    controllers.topic.PubTopicController.topVotedTopicByPubId(oper,aid,offset:Int,size:Int)

PUT           /api/topic/pub/vote/:oper/:aid/id/:tid                                                                     controllers.topic.PubTopicController.voteOnePubByTopicId(oper,aid,tid)

DELETE        /api/topic/pub/vote/:aid/id/:tid                                                                           controllers.topic.PubTopicController.unvoteOnePubByTopicId(aid,tid)
GET           /api/topic/pub/vote/:oper/:aid/id/:tid                                                                     controllers.topic.PubTopicController.nUserVotedByTopicId(oper,aid,tid)
GET           /api/topic/pub/voter/:oper/:aid/id/:tid/offset/:offset/size/:size                                          controllers.topic.PubTopicController.pubTopicVoterByTopicId(oper,aid,tid,offset:Int,size:Int)
GET           /api/topic/pub/voted/topic/rank/:oper/id/:tid/offset/:offset/size/:size                                    controllers.topic.PubTopicController.topVotedPubByTopicId(oper,tid,offset:Int,size:Int)
GET           /api/topic/pub/voted/topic/rank/:oper/id/:tid/offset/:offset/size/:size/voter/:maxVoter                    controllers.topic.PubTopicController.topVotedPubWithVoterByTopicId(oper,tid,offset:Int,size:Int,maxVoter:Int)


GET           /api/topic/pub/topics/:oper/:aid/toffset/:toffset/tsize/:tsize/uoffset/:uoffset/usize/:usize               controllers.topic.PubTopicController.findVotedTopicsAndUsersByPubId(oper,aid,toffset:Int,tsize:Int,uoffset:Int,usize:Int)


GET           /api/knowledge-graph/:entry                                                                                controllers.graph.KnowledgeGraphController.getGraph(entry)


# Fusion
POST          /api/fusion/person/merge/:mid                                                                              controllers.bifrost.PersonBifrostController.tryToDoMerge(mid)
GET           /api/fusion/person/pending/:channel/offset/:offset/size/:size                                              controllers.bifrost.PersonBifrostController.listMergeQueue(channel,offset:Int,size:Int)
GET           /api/fusion/person/request/:prqid                                                                          controllers.bifrost.PersonBifrostController.getMergeRequest(prqid)
POST          /api/fusion/person/request/:prqid                                                                          controllers.bifrost.PersonBifrostController.handleMergeRequest(prqid)

GET           /api/fusion/person/ctasks/email/:src/:size                                                                 controllers.bifrost.PersonBifrostController.listEmailCrawlTasks(src, size:Int)
GET           /api/fusion/person/ctasks/gender/:src/:size                                                                controllers.bifrost.PersonBifrostController.listGenderCrawlTasks(src, size:Int)

POST          /api/fusion/person/ctasks/email                                                                            controllers.bifrost.PersonBifrostController.crawledEmailUpdate
POST          /api/fusion/person/ctasks/gender                                                                           controllers.bifrost.PersonBifrostController.crawledGenderUpdate

POST          /api/fusion/pub/dc                                                                                         controllers.bifrost.PublicationBifrostController.checkByTitleAndFirstAuthor
POST          /api/fusion/pub/stnbh                                                                                      controllers.bifrost.PublicationBifrostController.searchTopNPubsByHash

# Bifrost
POST          /api/bifrost/person/merge/:mid                                                                             controllers.bifrost.PersonBifrostController.tryToDoMerge(mid)
GET           /api/bifrost/person/pending/:channel/offset/:offset/size/:size                                             controllers.bifrost.PersonBifrostController.listMergeQueue(channel,offset:Int,size:Int)
GET           /api/bifrost/person/request/:prqid                                                                         controllers.bifrost.PersonBifrostController.getMergeRequest(prqid)
POST          /api/bifrost/person/request/:prqid                                                                         controllers.bifrost.PersonBifrostController.handleMergeRequest(prqid)

GET           /api/bifrost/person/ctasks/email/:src/:size                                                                controllers.bifrost.PersonBifrostController.listEmailCrawlTasks(src, size:Int)
GET           /api/bifrost/person/ctasks/gender/:src/:size                                                               controllers.bifrost.PersonBifrostController.listGenderCrawlTasks(src, size:Int)

POST          /api/bifrost/person/ctasks/email                                                                           controllers.bifrost.PersonBifrostController.crawledEmailUpdate
POST          /api/bifrost/person/ctasks/gender                                                                          controllers.bifrost.PersonBifrostController.crawledGenderUpdate

POST          /api/bifrost/person/:id/hide                                                                               controllers.bifrost.PersonBifrostController.doHideOnePerson(id)
DELETE        /api/bifrost/person/:id/hide                                                                               controllers.bifrost.PersonBifrostController.undoHideOnePerson(id)

POST          /api/bifrost/pub/dc                                                                                        controllers.bifrost.PublicationBifrostController.checkByTitleAndFirstAuthor
POST          /api/bifrost/pub/stnbh                                                                                     controllers.bifrost.PublicationBifrostController.searchTopNPubsByHash

# this is just used to create a mention
POST          /api/bifrost/scholar/person-update                                                                         controllers.bifrost.PersonBifrostController.createPersonUpdateRequest

POST          /api/bifrost/person/create                                                                                 controllers.bifrost.PersonBifrostController.createPersons

# Bifrost, affs

POST          /api/bifrost/affs/merge/:mid                                                                               controllers.aff.AffiliationController.mergeAffs(mid)


# Reviewer
GET           /api/reviewer/network                                                                                      controllers.reviewer.ReviewerController.getReviewerNet
